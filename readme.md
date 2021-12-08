# 경희대학교 캡스톤디자인2 - 박기범

## 0. 프로젝트 소개
수많은 데이터들 중 소수의 특이상황이 드러난 이미지로부터 특이상황 영역 또는 특이상황이 포함된 이미지를 인식하기 위한 Feature를 고안한다. 그리고 이를 기반으로 적절한 Classifier (CNN 등)를 선정하고 인식을 다양하게 수행한다. 이후 그 성능을 평가하여 최종적으로 제시한 방법을 통해 Class imbalance problem을 해결하기 위해 적합한 데이터 증강(Data augmentation) 방법을 개발한다.

## 1. 진행상황
ver의 naming rule은 다음과 같습니다.
- ver x.y.z
    - x : 
        - 연구 방향의 변화 (ex borderline smote와 특정 오버샘플링 기법을 적용할 때, 그 순서의 변화에 따른 성능 차이 확인 -> borderline smote를 적용하고 다른 오버샘플링 기법을 적용할때, 가장 좋은 성능을 보이는 오버샘플링 기법 확인)
        - 연구 단계의 변화 (ex borderline smote와 특정 오버샘플링 기법을 적용할 때, 그 순서의 변화에 따른 성능 차이 확인 ->
        앞선 실험의 결과를 검증하기 위한 다음 실험을 진행)
    - y : 사용되는 라이브러리, 데이터셋의 변화
    - z : 동일한 방향, 동일한 라이브러리를 사용한 새로운 테스트


1.  ver 1.0.0 (11.09)
    - 프로젝트 구현물 생성 
    - 구글 colab과 sklearn, imblearn 라이브러리를 사용하여 신용카드 사기 데이터에 대한 over sampling 기법 수행
    - 다음의 시나리오 대로 over smapling을 사용하고 로지스틱 회귀를 통한 분류성능 비교
        - borderline-smote -> smote
        - smote -> borderline-smote

2. ver 1.1.0 (11.10)
    - 구글 colab 환경의 성능 부족 및 오류로 인한 데이터셋 변경
        - 기존에 사용했던 신용카드 사기 데이터에 대해 over sampling을 지속적으로 적용할 경우, 구글 colab의 성능제한에 의해 over sampling이 자꾸 멈춰버림.
        - 이에 따라, sklearn에서 제공하는 유명인 얼굴 사진 데이터로 변경하여 데이터 셋을 대폭 줄임 (총 데이터 수 :약 30만건 -> 약 600건)
    - 다음의 시나리오 대로 over smapling을 사용하고 로지스틱 회귀를 통한 분류성능 비교
        - borderline-smote -> adasyn
        - adasyn -> borderline-smote

3. ver 1.1.1 (11.15)
    - ver 1.1.0과 동일한 실험을 진행.
    - ver 1.1.0에서 사용한 adasyn 알고리즘을 다음의 알고라즘으로 변경하여 실험 진행
     - svm-smote
     - k-means smote

4. ver 2.0.0 (12.08)
    - borderline smote를 진행 후 다른 증강 기법을 적용했을 때 더 결과가 좋았던 원인을 분석
        - borderline smote에 관한 논문 리서치
        - 임의의 불균형 데이터를 생성하여 4가지 경우에 대해 오버샘플링 이후 경계선 데이터 개수를 직접 확인
            - borderline smote -> random over sampling
            - random over sampling -> borderline smote
            - borderline smote -> smote
            - smote -> borderline smote