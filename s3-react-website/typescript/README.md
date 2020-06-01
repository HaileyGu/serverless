# AWS S3 / React 웹사이트 패턴
React 애플리케이션을 변경없이 s3에 배포 할 수 있도록 AWS CDK와 React를 함께 패키징하였습니다.

### 이상적인 아키텍처:
![Architecture](https://raw.githubusercontent.com/cdk-patterns/serverless/master/s3-react-website/img/architecture.PNG)

### 이 패키지의 아키텍처:
이 패턴은 기본적으로 React 웹 사이트를 Amazon S3에 배포하지만 CloudFront, Route53 또는 Aws Certificate Manager는 설정하지 않습니다. 다음의 문서를 참고하면 어떻게 배포가 이루어지는지 알 수 있습니다.[cdk-spa-deploy docs](https://github.com/nideveloper/CDK-SPA-Deploy)

## S3 React 배포 패턴 분석
이 패키지의 기술적 이론 이나 코드, 그리고 이 패키지의 구현이 배포된 데모에 대해서 훑어보고 싶다면 아래의 영상을 참고하십시오:
[![Alt text](https://img.youtube.com/vi/tUUNiF0q7rk/0.jpg)](https://www.youtube.com/watch?v=tUUNiF0q7rk)

## 사용하는 방법
로컬 컴퓨터에 AWS를 환경 변수를 이미 설정했거나 cloud9에서 작업하는 경우, 단순히 다음의 두 명령어를 사용하여 웹사이트를 배포할 수 있습니다. (명령어는 README.md 파일이 위치하고 있는 곳에서 실행해야 합니다.):
- cd website && npm i && npm run build
- cd ../cdk && npm i && npm run build && npm run deploy 

## 프로젝트 구조

### React 웹사이트 (/website)
웹사이트의 코드는 website 폴더에 있습니다. 이것은 npx create-react-app라는 명령어를 통해서 생성된 비어있는 웹사이트입니다.

#### 몇몇 명령어들
- npm install
- npm run build
- npm run start

### CDK S3 인프라 배포 (/cdk)
CDK 코드는 cdk 폴더에 있으며, 웹 사이트 배포를 위한 S3 버킷을 설정하고 website 폴더에 있는 React 웹 사이트를 업로드합니다. 이것은 JSII 컨스 트럭 타를 사용합니다 -
https://www.npmjs.com/package/cdk-spa-deploy

초기 설정은 cloudfront를 사용하지 않지만 cdk-spa-deploy 모듈은 클라우드 프론트 및 사용자 정의 도메인을 추가하는 것이 얼마나 쉬운 지 자세히 설명합니다.

#### 유용한 명령어드

- npm run build
- cpm run cdk synth - 콘솔에 cloudformation을 출력합니다.
- npm run deploy - website 폴더를 빌드 한 후 s3에 배포합니다.

### buildspec.yml
AWS의 codebuild 리소스를 설정하여 프로젝트를 자동으로 빌드/배포하려는 경우를 위해 아 파일을 포함 시켜두었습니다.