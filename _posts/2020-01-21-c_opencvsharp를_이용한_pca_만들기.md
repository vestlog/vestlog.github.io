---
title:  "[2020-01-21] - [C#] OpenCvSharp를 이용한 PCA 만들기"
categories:
  - Blog
tags:
  - "pca"
  - "판별"
  - "분석"
  - "학습"
  - "매칭"
  - "c#"
  - "검출"
  - "opencv"
  - "opencvsharp"
last_modified_at: 2025-05-30T16:03:59+09:00
---

## [C#] OpenCvSharp를 이용한 PCA 만들기

코딩정보/OpenCv

2020-01-21 09:29:21

* * *

안녕하세요

이번 시간 포스팅할 부분은 OpenCvSharp를 이용한 PCA(Principal Component Analysis)를 구현해 볼려고 합니다

근데 아무 저와 똑같이 PCA가 뭐지??라는 분들이 많으실거 같아서 검색을 통해 제가 알아본 내용을

간략하게 소개 하고 구현 해보도록 할께요

# ▶ 주성분분석(Principal Component Analysis)

\- PCA는 분포된 데이터들의 주성분(Principal Component)를 찾아 고차원의 데이터를 저차원의 데이터로 환원

시키는 기법

음... 정의를 보아도 무슨말인지 잘 이해가 되지 않습니다. 제가 이해한것을 표현하자면 어떤한 데이터의 주성분을

분석하여 데이터로 환원한뒤 그 환원된 값의 분포도에 따라 어떠한 형태를 띄고 있는지를 보는 거라고 이해하고

있는데 이게 맞는것인지를 모르겠습니다

제가 이해한 정의를 가지고 프로그래밍을 분석하여 구현하였는데

프로그램적 순서를 보면 이렇습니다

① 원본 이미지

② 대상 이미지

③ 형상 비교를 통한 매치율 분석

이론은 간단하지만 구현하고 분석을 쉽지가 않더라구요 아무 저도 프로그래머다 보니 논리적 이론 보다는

프로그램적 구현쪽을 더 많이 파고 있는 입장이라 완벽한 설명은 불가합니다

좀 더 구체적 이해와 설명이 필요하시면 검색을 통해 이해 하시는게 좋을거 같습니다

그럼 다시 본론으로 돌아와서 프로그램 구현을 시작해 보겠습니다

해당 포스팅의 글 역시 기존 OpenCvSharp 포스팅 자료와 이어서 진행되오니

이해가 안가거나 중간 생략된 부분은 이전 포스팅을 참조하시기 바랍니다

<https://codingman.tistory.com/49>

[ [C#]OpenCvSharp 라이브러리 사용하기 #1 안녕하세요 저번 포스팅에 C#으로 OpenCvSharp 라이브러리를 등록하여
구현하는 포스팅을 준비하던중에 OpenCv 3,4 버전에서 오류가 발생하는 문제가 있다는 얘길 듣고 부랴부랴 포스팅 내용을 검토해봤는데
역시.. codingman.tistory.com ](https://codingman.tistory.com/49)

그럼 프로그램 동작을 위한 디자인 부분부터 설명하겠습니다

[디자인]

\- 메뉴에 머쉰런닝 탭에 PCA 버튼을 만들고 학습과 검출의 세부 버튼을 생성합니다

![](/assets/images/c_opencvsharp를_이용한_pca_만들기/img.jpg)

\- 학습과 검출 세부 버튼에 클릭시 동작 할 수 있도록 이벤트를 활성화 시킵니다

![](/assets/images/c_opencvsharp를_이용한_pca_만들기/img_1.jpg)
![](/assets/images/c_opencvsharp를_이용한_pca_만들기/img_2.jpg)

\- 해당 이벤트에 다음과 같이 코딩합니다

* 학습
    
    
            private void 학습ToolStripMenuItem1_Click(object sender, EventArgs e)
            {
                using (PCA pca = new PCA())
                using (IplImage temp = pca.LearnPCA())
                {
                    if (temp == null)
                    {
                        MessageBox.Show("데이타 파일 오류");
                        return;
                    }
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
            }

*검출
    
    
            private void 검출ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (PCA pca = new PCA())
                {
                    String[] temp = pca.recognize();
                    if (temp == null) MessageBox.Show("오류발생 확인요망");
                    for (int i = 0; i < temp.Length; i++)
                        listBox1.Items.Add(temp[i]);
    
                }
            }

\- PCA 기능 동작을 위한 클래스 파일 생성합니다

![](/assets/images/c_opencvsharp를_이용한_pca_만들기/img_3.jpg)

\- 생성된 클래스에 다음과 같이 소스코드를 작성 합니다

    
    
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.IO;
    using OpenCvSharp;
    
    namespace OpenCV_V1
    {
        class PCA : IDisposable
        {
            #region 초기값
            int nTrainFaces = 0;
            int nEigens = 0;
    
            IplImage result;
            IplImage[] faceImgArr;
            IplImage[] eigenVectArr;
            IplImage pAvgTrainImg;
            float[,] projectedTrainFaceMat;
            float[] eigenValMat;
            CvMat personNumTruthMat;
    
            public void Dispose()
            {
                if (result != null) Cv.ReleaseImage(result);
                if (!pAvgTrainImg.IsDisposed) pAvgTrainImg.Dispose();
                if (!faceImgArr[0].IsDisposed)
                {
                    for (int i = 0; i < nTrainFaces; i++)
                    {
                        faceImgArr[i].Dispose();
                    }
                }
                if (!eigenVectArr[0].IsDisposed)
                {
                    for (int i = 0; i < nEigens; i++)
                        eigenVectArr[i].Dispose();
                }
                if (!personNumTruthMat.IsDisposed) Cv.ReleaseMat(personNumTruthMat);
            }
            #endregion
    
            #region PCA 학습
    
            public unsafe IplImage LearnPCA()
            {
                //학습할 이미지 사진 파일명을 나열한 텍스파일 읽기
                nTrainFaces = loadFaceImgArray("train.txt");
                if (nTrainFaces < 2)
                {
                    //MessageBox.Show("데이타 파일이 잘못 되었슴");
                    return null;
                }
    
                doPCA();
    
                projectedTrainFaceMat = new float[nTrainFaces, nEigens];
                float[] tempProject = new float[nEigens];
    
                for (int i = 0; i < nTrainFaces; i++)
                {
                    Cv.EigenDecomposite(faceImgArr[i], eigenVectArr, pAvgTrainImg, tempProject);//projectedTrainFaceMat[i]);
                    projectedTrainFaceMat[i, 0] = tempProject[0];
                    projectedTrainFaceMat[i, 1] = tempProject[1];
                }
    
    
                storeTraingData();
                return result;
            }
    
            private int loadFaceImgArray(String file)
            {
                //텍스트 파일에 나열되어진 파일명대로 이미지 읽어서 메모리에 저장하기   
                int i = 0;
                string[] lines = File.ReadAllLines(file); //학습할 파일명 획득
                faceImgArr = new IplImage[lines.Length]; //학습할 얼굴 갯수만큼 메모리 확보
    
                foreach (string line in lines) //텍스트 파일에서 읽은 파일명으로
                {
                    faceImgArr[i] = new IplImage(lines[i], LoadMode.GrayScale); //사진이미지 읽어 오기
                    i++;
                }
                return lines.Length;
    
            }
    
            private unsafe void doPCA()
            {
                CvTermCriteria calcLimit;
                CvSize faceImgSize;
                nEigens = nTrainFaces - 1;
    
                faceImgSize.Width = faceImgArr[0].Width;
                faceImgSize.Height = faceImgArr[0].Height;
    
                eigenVectArr = new IplImage[nEigens];
    
                for (int i = 0; i < nEigens; i++)
                    eigenVectArr[i] = new IplImage(faceImgSize, BitDepth.F32, 1);
    
                eigenValMat = new float[nEigens];
                pAvgTrainImg = new IplImage(faceImgSize, BitDepth.F32, 1);
                calcLimit = new CvTermCriteria(CriteriaType.Iteration, nEigens, 1);
                Cv.CalcEigenObjects(faceImgArr, eigenVectArr, 0, calcLimit, pAvgTrainImg, eigenValMat);
    
            }
    
            //학습된 데이타 저장하기
            private void storeTraingData()
            {
                int[] faceID = { 1, 2, 4, 5 };//사실은 텍스트 파일에 같이 써야 하지만 분리하기 귀찮아서
                personNumTruthMat = new CvMat(1, nTrainFaces, MatrixType.S32C1, faceID);
    
                using (CvFileStorage fs = new CvFileStorage("facedata.xml", null, FileStorageMode.Write))
                using (CvMat eigen = new CvMat(1, nEigens, MatrixType.F32C1, eigenValMat))
                using (CvMat projected = new CvMat(nTrainFaces, nEigens, MatrixType.F32C1, projectedTrainFaceMat))
                {
                    fs.WriteInt("nEigens", nEigens);
                    fs.WriteInt("nTrainFaces", nTrainFaces);
                    fs.Write("trainPersonNumMat", personNumTruthMat);
                    fs.Write("eigenValMat", eigen);
                    fs.Write("projectedTrainFaceMat", projected);
                    fs.Write("avgTrainImg", pAvgTrainImg);
    
                    for (int i = 0; i < nEigens; i++)
                    {
                        String varName = String.Format("eigenVect_{0}", i);
                        fs.Write(varName, eigenVectArr[i]);
                    }
                    result = new IplImage(pAvgTrainImg.Size, BitDepth.U8, 1);
                    //Currentley, bitmap converter can read not only BitDeth.U8 but also 32F
                    Cv.CvtScale(pAvgTrainImg, result);
                }
            }
            #endregion
    
            #region PCA 인식
    
            public unsafe String[] recognize()
            {
                String[] str;
    
                int nTestFaces = 0; //비교할 이미지 숫자
                CvMat trainPersonNumMat; //학습으로 저장된
                float[] projectedTestFace;
    
                nTestFaces = loadFaceImgArray("test.txt"); //얼굴갯수 리턴
                projectedTestFace = new float[nEigens];
    
                if (!loadTranningData(out trainPersonNumMat)) return null;
    
                projectedTrainFaceMat = new float[trainPersonNumMat.Rows, trainPersonNumMat.Cols];//배열확보
                float[] tempProject = new float[nEigens];
    
                for (int i = 0; i < trainPersonNumMat.Rows; i++)
                    for (int j = 0; j < trainPersonNumMat.Cols; j++)
                        projectedTrainFaceMat[i, j] = (float)Cv.mGet(trainPersonNumMat, i, j); //저장된 값 이동
    
                str = new String[nTestFaces]; //비교할 파일 갯수 만큼
    
                for (int i = 0; i < nTestFaces; i++)
                {
                    int iNearest, nearest, truth;
    
                    Cv.EigenDecomposite(faceImgArr[i], eigenVectArr, pAvgTrainImg, tempProject);
    
                    iNearest = findNearestNeighbor(tempProject); //근접도
                    truth = (int)Cv.mGet(personNumTruthMat, 0, i); //실제 명기된 ID
                    nearest = (int)Cv.mGet(personNumTruthMat, 0, iNearest);
    
                    str[i] = String.Format("nearest ID ={0}, Real ID = {1}", nearest, truth);
    
                }
                return str;
    
    
            }
    
            private int findNearestNeighbor(float[] projecTestFace)
            {
                double leastDistSq = 1e12;// DBL_MAX;
                int iTrain, iNearest = 0;
    
                for (iTrain = 0; iTrain < nTrainFaces; iTrain++) //비교할 얼굴 갯수
                {
                    double distSq = 0;
    
                    for (int i = 0; i < nEigens; i++)
                    {
                        float d_i = projecTestFace[i] - projectedTrainFaceMat[iTrain, i];//학습 파일에서 읽은 값과
                        //distSq += d_i*d_i / eigenValMat->data.fl;  // 마할노비스 거리
                        distSq += d_i * d_i; // 유클리디안 거리
                    }
    
                    if (distSq < leastDistSq) //더 근접한 값이 있는지 찾음
                    {
                        leastDistSq = distSq;
                        iNearest = iTrain;     //몇번째 얼굴인지
                    }
                }
                return iNearest;
            }
    
            //저장된 학습 데이타 읽어 오기
            private bool loadTranningData(out CvMat pTrainPersonNumMat)
            {
                CvFileNode param;
    
                using (CvFileStorage fs = new CvFileStorage("facedata.xml", null, FileStorageMode.Read))
                {
                    pTrainPersonNumMat = null;
                    if (fs == null) return false;
    
                    nEigens = fs.ReadIntByName(null, "nEigens");//고유치
                    nTrainFaces = fs.ReadIntByName(null, "nTrainFaces"); //학습 갯수
                    param = Cv.GetFileNodeByName(fs, null, "trainPersonNumMat");
                    personNumTruthMat = fs.Read<CvMat>(param); //얼굴ID
    
                    param = Cv.GetFileNodeByName(fs, null, "projectedTrainFaceMat");//학습된 값
                    pTrainPersonNumMat = fs.Read<CvMat>(param);
    
                    param = Cv.GetFileNodeByName(fs, null, "avgTrainImg"); //학습한 평균 이미지
                    pAvgTrainImg = fs.Read<IplImage>(param);
                    eigenVectArr = new IplImage[nEigens];
                    for (int i = 0; i < nEigens; i++)
                    {
                        String varName = String.Format("eigenVect_{0}", i);
                        param = Cv.GetFileNodeByName(fs, null, varName);
                        eigenVectArr[i] = fs.Read<IplImage>(param);
                    }
    
                }
                int[] faceID = { 1, 2, 4, 5, 1, 2, 4, 5, 1, 2, 4, 5, 1, 2, 4, 5, 1, 2, 4, 5, 1, 2, 4, 5 };//사실은 텍스트 파일에 같이 써야 하지만 분리하기 귀찮아서
                personNumTruthMat = new CvMat(1, nTrainFaces, MatrixType.S32C1, faceID);//ID 배정
    
                return true;
            }
            #endregion
        }
    }
    

\- 해당 클래스가 정상 동작을 하기 위한 기초 첨부파일을 다운 받습니다

[ S1245_XML.zip 0.39MB ](./file/S1245_XML.zip)

\- 첨부파일의 내용을 Debug 폴더에 붙여 넣기 합니다

*첨부파일 내용

1) s1,s2,s4,s5 비교 그룹 이미지 (형식 : bpm)

(샘플 얼굴 이미지 사진 입니다)

2) test.txt

: 그룹에 포함되어 있는 파일 정보

3) train.txt

: 그룹에 대표 이미지 지정

3) facedata.xml

: 학습 정보 기록을 위한 xml

\- 실행 한뒤 각 그룹 이미지 폴더에서 1.bpm을 불러와 검출을 시도합니다

[결과 창]

![](/assets/images/c_opencvsharp를_이용한_pca_만들기/img_4.jpg)

\- 저는 샘플 사진으로 트와이스 맴버를 bpm으로 전환하여 비교 하여 다른 얼굴들과 어느정도 분석이 가능한지

테스트를 해봤습니다(좋아하니깐!)

\- 쯔위는 s5 그룹에 대표입니다

\- 좌측 listBox1의 결과를 분석하면 해당 폴더의 그룹별 매칭 상태가 나타나는데 90%로 정도 쯔위를 판별해

내는것을 볼수 있습니다

\- 해당 자료를 구현하여 다른 샘플을 통해 다른 각도로 수정하여 응용해 보시기 바랍니다

  

#pca #판별 #분석 #학습 #매칭 #c# #검출 #opencv #opencvsharp

