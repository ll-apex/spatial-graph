# RDF 그래프 시작하기

## 소개

이 실습에서는 RDF 데이터를 Autonomous Database에 연결될 버킷에 업로드하여 시작하는 단계를 안내합니다. 이 작업을 수행하려면 프로파일에서 올바른 OCI 사용자 이름을 복사해야 합니다. Graph Studio가 OCI Object Storage의 RDF 데이터에 액세스할 수 있게 하려면(DBMS\_CLOUD 패키지 사용) OCI 계정을 사용하여 액세스 토큰을 생성해야 합니다. 이것은 보조 실습에서 사용됩니다.

예상 시간: 5분

### 목표

*   OCI 오브젝트 스토리지로 RDF 데이터 업로드
*   OCI 사용자 이름 보기
*   접근 토큰 생성

### 필요 조건

이 실습에서는 다음을 가정합니다.

*   Oracle Cloud 계정
*   이 [링크](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt)를 사용하여 MOVIESTREAM 파일(moviestream\_rdf.nt)을 다운로드합니다.

## **작업 1:** OCI Object Storage에 RDF 데이터 업로드

1.  Oracle Cloud 인증서를 사용하여 OCI 콘솔에 사인인합니다.
2.  탐색 메뉴를 열고 Storage를 누릅니다. Object Storage & Archive Storage에서 다음과 같이 Buckets를 누릅니다. ![메뉴에서 버킷 폴더가 선택되는 위치를 설명하는 이미지](./images/buckets-folder.png)
3.  OCI 계정에 적용되는 구획을 선택합니다. ![버킷 페이지에서 구획 드롭다운 메뉴의 위치를 보여주는 이미지](./images/compartment-menu.png)
4.  Create Bucket을 누릅니다. 다음과 같이 Create Bucket(버킷 만들기) 슬라이더가 열립니다. ![버킷 생성 페이지를 설명하는 이미지](./images/create-bucket.png)
5.  버킷 이름을 입력하고 나머지는 모두 기본값으로 두고 Create를 누릅니다. 버킷이 생성되어 버킷 페이지에 다음과 같이 나열됩니다. ![버킷 생성 결과를 보여주는 이미지](./images/bucket-result.png)
6.  RDF\_DATA\_BUCKET 링크를 누르고 Bucket Details 페이지로 이동합니다.

![생성 후 버킷 페이지를 보여주는 이미지입니다.](./images/bucket-page.png) 7. Objects 섹션에서 Upload를 누릅니다. 객체 업로드 슬라이더가 열립니다. 8. 로컬 시스템에서 다운로드한 RDF moviestream\_rdf.nt 파일 [링크](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt)를 선택하고 Upload를 누릅니다. 파일이 성공적으로 업로드됩니다. Close를 눌러 Bucket Details 페이지로 돌아갑니다. 업로드된 파일은 다음과 같이 객체 아래에 나열됩니다. ![버킷에 업로드된 객체를 보여주는 이미지](./images/image-upload.png)

1.  업로드된 파일의 \[작업\] 메뉴를 선택하고 \[객체 세부정보 보기\]를 눌러 업로드된 파일의 속성에 액세스합니다. 다음과 같이 Object Details 슬라이더가 열립니다. ![객체 세부정보 보기 옵션이 강조 표시된 객체 메뉴를 보여주는 이미지](./images/object-details.png)
2.  객체의 URL 경로를 기록해 둡니다. Graph Studio의 RDF 임포트 마법사에서 사용됩니다. ![버킷에서 객체에 대한 URL 경로를 찾을 위치를 보여주는 이미지](./images/url-path.png)

## **작업 2:** OCI 사용자 이름 보기

1.  오른쪽 상단 모서리에 있는 아바타 아이콘을 눌러 프로파일을 엽니다. 프로파일 아래의 첫번째 항목은 OCI 사용자 이름입니다. ![OCI 프로파일에 액세스하는 방법을 보여주는 이미지](./images/oci-profile.png)
2.  OCI 사용자 이름을 기록해 둡니다. Graph Studio의 RDF 임포트 마법사에서 사용됩니다. ![사용자 세부정보의 OCI 사용자 이름을 보여주는 이미지입니다.](./images/oci-username.png)

## **작업 3:** OCI 콘솔에서 액세스 토큰 생성

1.  Oracle Cloud 인증서를 사용하여 OCI 콘솔에 사인인합니다.
    
2.  오른쪽 상단 모서리에 있는 아바타 아이콘을 눌러 프로파일을 열고 사용자 설정을 누릅니다. ![프로파일에서 사용자 설정에 액세스하는 방법을 보여주는 이미지](./images/user-settings.png)
    
3.  다음과 같이 Resources 아래의 Auth Tokens를 누릅니다. ![사용자 설정의 리소스 메뉴에서 인증 토큰에 액세스하는 방법을 보여주는 이미지](./images/auth-tokens.png)
    
4.  Generate Token을 누릅니다. \[토큰 생성\] 대화상자가 열립니다. ![인증 토큰 생성 방법을 보여주는 이미지](./images/gen-tokens.png)
    
5.  설명을 입력하고 토큰 생성을 누릅니다. 생성된 토큰 세부정보가 다음과 같이 표시됩니다. ![생성된 인증 토큰 복사 방법을 보여주는 이미지](./images/token-details.png)
    
6.  복사를 눌러 토큰을 복사하고 나중에 사용할 수 있도록 저장합니다.
    

이 연습을 마칩니다. _이제 다음 실습을 진행할 수 있습니다._

## 확인

*   **작성자** - Melliyal Annamalai, Distinguished Product Manager
*   **기술 기여자** - Nicholas Cusato, Santa Monica Specialist Hub
*   **최종 업데이트 수행자/날짜** - Nicholas Cusato, Santa Monica Specialist Hub, 2022년 2월 25일