---

copyright:
  years: 2016, 2019
lastupdated: "2019-2-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}


# Delivery Pipeline 개요
{: #deliverypipeline_about}

{{site.data.keyword.contdelivery_full}}에는 사용자 개입을 최소화하여 반복할 수 있는 방식으로 빌드, 테스트, 배치를 수행하는 Delivery Pipeline이 포함됩니다. 파이프라인에서는 일련의 단계에서 입력을 검색하고 작업(예: 빌드, 테스트 및 배치)을 실행합니다.
{:shortdesc}

파이프라인을 보거나 수정하거나 실행할 권한은 파이프라인을 소유한 도구 체인의 액세스 제어를 기반으로 합니다. 도구 체인의 액세스 제어에 대한 자세한 정보는 [리소스 그룹의 도구 체인에 대한 액세스 관리](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-toolchains-using#managing_access_resource_groups){: new_window} 및 [Cloud Foundry 조직의 도구 체인에 대한 액세스 관리](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-toolchains-using#managing_access_orgs){: new_window}를 참조하십시오.
{: important}

파이프라인에서 제공하는 다수의 작업 유형에서 실행될 스크립트를 지정하여 작업에 의해 실행되는 작업을 직접 제어할 수 있습니다. 이러한 스크립트는 {{site.data.keyword.Bluemix_notm}} 런타임과 상호작용하는데 필요한 도구를 포함한 많은 표준 개발 도구를 포함하고 있는 Docker 이미지에서 실행됩니다. 표준 Docker 이미지에 포함된 항목에 대한 자세한 정보는 [사전 설치된 리소스](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-deliverypipeline_environment#deliverypipeline_resources){: new_window}를 참조하십시오. 작업에 표준 이미지에서 사용할 수 없는 개발 도구가 필요하거나 해당 도구의 다른 버전이 필요한 경우 사용자 정의 이미지를 사용할 수 있습니다. 사용자 정의 이미지에 대한 자세한 정보는 [사용자 정의 Docker 이미지에 대한 작업](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-custom_docker_images#custom_docker_images){: new_window}을 참조하십시오.

파이프라인에서 스크립트를 실행하면 작업이 실행되고 있는 컨텍스트를 설명하는 특성은 환경 변수를 사용하여 스크립트에 전달됩니다. 예를 들면, 단계에 대한 입력인 저장소의 URL, 실행되고 있는 단계와 작업의 이름, 작업 유형에 의해 지정된 매개변수 등입니다. 사용 가능한 환경 변수 목록을 보려면 [사전 설치된 리소스](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-deliverypipeline_environment#deliverypipeline_resources)를 참조하십시오. 

파이프라인 레벨과 단계 레벨 모두에 특성을 정의할 수 있습니다. 파이프라인 특성은 파이프라인의 모든 단계와 작업에서 공유됩니다. 단계 특성은 특정 단계에 고유하며 해당 단계의 모든 작업에서 공유됩니다. 특성에 대한 자세한 정보는 [환경 특성(환경 변수)](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-deliverypipeline_about#environment_properties)을 참조하십시오.

## 단계
{: #deliverypipeline_stages}

단계는 코드가 빌드, 배치 및 테스트됨에 따라 입력 및 작업을 구성합니다. 단계에서는 소스 제어 저장소(SCM 저장소) 또는 다른 단계에 있는 빌드 작업의 입력을 승인합니다. SCM 저장소의 경우 입력은 저장소의 특정 분기 컨텐츠입니다. 빌드 작업의 경우 입력은 작업에 의해 생성되는 아티팩트입니다. 첫 번째 단계를 작성할 때 **입력** 탭에 기본 설정이 포함되어 있습니다.

단계가 실행되면 해당 단계의 입력사항이 해당 단계의 각 작업에 전달됩니다. 각 작업에는 실행할 클린 컨테이너가 제공됩니다. 결과적으로 단계 내에 있는 작업에서는 아티팩트를 서로 전달할 수 없습니다. 작업 간의 아티팩트를 전달하려면 작업을 두 단계로 분리하고 첫 번째 단계에서의 작업 출력을 두 번째 단계에 대한 입력으로 사용하십시오.
{: tip}

파이프라인 특성을 정의할 수 있는 방법과 유사하게 특정 단계의 모든 작업에 사용할 단계 특성을 정의할 수도 있습니다. 예를 들어, `TEST_URL` 특성을 정의하여 단계에서 URL을 배치 및 테스트 작업에 전달할 수 있습니다. 배치 작업에서는 해당 URL에 배치하고 테스트 작업에서는 해당 URL에서 실행 앱을 테스트합니다. 단계 특성도 환경 변수를 사용하여 작업 스크립트에 전달됩니다. 파이프라인 레벨과 단계 레벨 모두에 동일한 특성이 정의되면 단계 특성의 값이 사용됩니다.

기본적으로 한 단계에서, 변경사항이 프로젝트의 SCM 저장소로 전달될 때마다 빌드 및 배치가 자동으로 실행됩니다. 단계 및 작업은 직렬로 실행되므로 작업 플로우를 제어할 수 있습니다. 예를 들어, 배치 단계 앞에 테스트 단계를 놓을 수 있습니다. 테스트 단계의 테스트가 실패하면 배치 단계가 실행되지 않습니다.

특정 단계를 면밀히 제어할 수 있습니다. 해당 입력에서 변경이 발생할 때마다 단계가 실행되도록 하지 않으려면 해당 기능을 사용 불가능하게 설정하십시오. **입력** 탭의 단계 트리거 섹션에서 **이 단계를 수동으로 실행할 때만 작업 실행**을 클릭하십시오.

![입력 탭](images/input_tab_only_execute.png)


### 빌드 단계
{: #build_stage}

빌드 단계는 아티팩트 빌드 방법을 표시하기 위해 **빌더 유형**을 지정합니다.  

빌드 작업에서 사용 가능한 필드 중 다수는 다중 빌더 유형 전체에서 공통입니다.
{: tip}

다음 빌더 유형을 사용할 수 있습니다.

* **단순** - **단순** 빌더 유형을 사용하는 작업에서는 현재 단계의 입력사항을 사용하며 수정하지 않고 향후 단계에서 사용하도록 아카이브합니다. 일반적으로 **단순** 빌더 유형은 SCM 저장소에서의 단계 입력인 경우에만 유용합니다.
* **Ant** - Apache Ant 파일을 사용하여 빌드 작업을 관리하려면 이 빌드 유형을 사용하십시오.
  * **빌드 스크립트** - 이 빌더 유형은 유효한 빌드 스크립트일 수 있습니다. 기본적으로 이 빌더 유형은 'ant'로 설정됩니다.
  * **작업 디렉토리** - 스크립트가 실행되는 디렉토리를 지정합니다.
  * **빌드 아카이브 디렉토리** - 후속 단계에서 사용하도록 아카이브할 작업 출력이 포함되는 디렉토리를 지정합니다.
  * **테스트 보고서 사용** - 빌드 작업에서 JUnit XML 형식으로 결과 파일을 생성하는 테스트를 실행하도록 지정하려면 이 선택란을 선택하십시오. 결과 파일을 기반으로 한 보고서가 작업 결과 페이지의 테스트 탭에 표시됩니다. 테스트에 실패한 경우 작업은 실패로 표시됩니다.
  * **코드 적용 범위 보고서 사용** - 코드 적용 범위 보고서에 사용할 수 있는 추가 필드를 표시하려면 이 선택란을 선택하십시오. 작업 디렉토리와 관련한 적용 범위 실행자(예: Istanbul, JaCoCo, ore Cobertura), 적용 범위 결과 파일의 위치 및 적용 범위 결과 디렉토리를 지정할 수 있습니다.
* **Container Registry**
* **Gradle(Artifactory, Nexus 또는 SonarQube)**
* **Grunt**
* **IBM Globalization Pipeline**
* **Maven(Artifactory, Nexus 또는 SonarQube)**
* **npm(Artifactory 또는 Nexus)**
* **Shell Script**

### 배치 단계
배치 단계는 빌드 단계의 입력을 지정합니다.  배치 단계의 작업은 **배치자 유형**을 지정합니다.  다음 배치자 유형을 사용할 수 있습니다.

1. **Cloud Foundry**
2. **Kubernetes**

## 작업
{: #deliverypipeline_jobs}

작업은 단계 내의 실행 단위입니다. 단계에는 여러 작업이 포함될 수 있으며, 단계 내의 작업은 순차적으로 실행됩니다. 기본적으로 하나의 작업이 실패하면 단계 내의 후속 작업이 실행되지 않습니다.

![단계 내의 빌드 및 테스트 작업](images/jobs.png)

작업은 각 파이프라인 실행을 위해 작성된 Docker 컨테이너 내의 개별 작업 디렉토리에서 실행됩니다. 작업이 실행되기 전에 해당 작업 디렉토리는 단계 레벨에서 정의된 입력으로 채워집니다. 예를 들어, 하나의 테스트 작업과 하나의 배치 작업을 포함하는 단계가 있을 수 있습니다. 하나의 작업에 종속 항목을 설치하는 경우 다른 작업에서는 이를 사용할 수 없습니다. 그러나 단계의 입력에서 종속 항목을 사용 가능하게 설정하면 두 작업 모두 해당 종속 항목을 사용할 수 있습니다.

단순 유형 빌드 작업을 제외하곤, 작업을 구성할 때 빌드, 테스트 또는 배치 명령이 포함된 UNIX 쉘 스크립트를 포함시킬 수 있습니다. 작업은 임시 컨테이너에서 실행되므로 작업이 같은 단계에 속하는 경우에도 한 작업의 조치는 다른 작업의 실행 환경에 영향을 미칠 수 없습니다.

샘플 빌드 및 배치 스크립트는 [https://github.com/open-toolchain/commons](https://github.com/open-toolchain/commons)에서 찾을 수 있습니다.

또한 파이프라인 작업은 `sudo`로서 다음 명령만 실행할 수 있습니다.
  * `/usr/sbin/service`
  * `/usr/bin/apt-get`
  * `/usr/bin/apt-key`
  * `/usr/bin/dpkg`
  * `/usr/bin/add-apt-repository`
  * `/opt/IBM/node-v0.10.40-linux-x64/npm`
  * `/opt/IBM/node-v0.12.7-linux-x64/npm`
  * `/opt/IBM/node-v4.2.2-linux-x64/npm`
  * `/usr/bin/Xvfb`
  * `/usr/bin/pip`


작업이 실행된 후에는 그 작업을 위해 작성된 컨테이너가 버려집니다. 작업 실행의 결과는 유지될 수 있지만 작업이 실행된 환경은 유지되지 않습니다.

작업은 최대 60분 동안 실행될 수 있습니다. 작업이 이 한계를 초과하면 작업이 실패합니다. 하나의 작업이 이 한계를 초과하는 경우에는 작업을 여러 개의 작업으로 나누십시오. 예를 들어, 작업이 세 개의 태스크를 수행하는 경우 이 작업을 세 개의 작업(태스크당 하나의 작업)으로 나눌 수 있습니다.
{: tip}

단계에 작업을 추가하는 방법을 알아보려면 [단계에 작업 추가](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-deliverypipeline_build_deploy#deliverypipeline_add_job){: new_window}를 참조하십시오.

### 빌드 작업

빌드 작업은 배치를 준비하기 위해 프로젝트를 컴파일합니다. 빌드 작업은 빌드 아카이브 디렉토리로 전송할 수 있는 아티팩트(기본적으로 프로젝트의 루트 디렉토리에 배치됨)를 생성합니다.

빌드 작업에서 입력되는 작업은 빌드 아티팩트를 작성 시와 동일한 구조로 참조해야 합니다. 예를 들어, 빌드 작업이 빌드 아티팩트를 `output` 디렉토리에 아카이브하는 경우 배치 스크립트는 프로젝트 루트 디렉토리가 아니라 `output` 디렉토리를 참조하여 컴파일된 프로젝트를 배치합니다.  **아카이브 디렉토리 빌드** 필드에 디렉토리 이름을 입력하여 아카이브할 디렉토리를 지정할 수 있습니다. 필드를 공백으로 두면 루트 디렉토리를 아카이브합니다.

**단순** 빌더 유형을 사용하는 경우 코드가 컴파일되거나 빌드되지 않습니다. 다음 단계를 위해 패키지되고 사용 가능하도록 설정됩니다.
{: tip}

Cloud Foundry를 사용하여 배치할 때 Cloud Foundry에는 올바른 아티팩트가 포함되어 앱을 실행할 수 있습니다. 자세한 정보는 [cf 명령을 사용하여 애플리케이션 배치](/docs/cloud-foundry?topic=cloud-foundry-deploy-apps#dep_apps)를 참조하십시오. Cloud Foundry 앱의 파이프라인에는 cf 명령을 실행하는 배치 단계가 포함됩니다.

Cloud Foundry는 [사용할 빌드팩을 발견하려고 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://docs.cloudfoundry.org/buildpacks/detection.html) 시도합니다. 앱의 루트 폴더에 있는 Manifest 파일에 사용할 [빌드팩](/docs/cloud-foundry-public?topic=cloud-foundry-public-using_buildpacks#using_buildpacks)을 지정할 수 있습니다. 일반적으로 빌드팩은 사용자 제공 아티팩트를 확인하여 다운로드할 종속 항목 및 바인딩 서비스와 통신하기 위한 애플리케이션 구성 방법을 결정할 수 있습니다. Manifest 파일에 대한 자세한 정보는 [Application Manifest](/docs/cloud-foundry?topic=cloud-foundry-deploy-apps#appmanifest)를 참조하십시오.

### 배치 작업

배치 작업은 프로젝트를 {{site.data.keyword.Bluemix_notm}}에 앱으로 업로드하며, URL에서 액세스할 수 있습니다. 프로젝트가 배치되고 나면 배치된 앱을 {{site.data.keyword.Bluemix_notm}} 대시보드에서 찾을 수 있습니다.

배치 작업은 새 앱을 배치하거나 기존 앱을 업데이트할 수 있습니다. 처음에 다른 방법(예: Cloud Foundry 명령행 인터페이스 또는 Web IDE의 실행 표시줄)을 사용하여 앱을 배치한 경우에도 배치 작업을 사용하여 앱을 업데이트할 수 있습니다. 앱을 업데이트하려면 배치 작업에서 해당 앱의 이름을 사용하십시오.

하나 또는 다수의 지역과 서비스에 배치할 수 있습니다. 예를 들면, {{site.data.keyword.deliverypipeline}}이 하나 이상의 서비스를 사용하고 한 지역에서 테스트되며 여러 지역의 프로덕션에 배치되도록 설정할 수 있습니다.

### 테스트 작업
조건이 충족되도록 하려면 빌드 및 배치 작업의 앞이나 뒤에 테스트 작업을 포함시키십시오. 필요에 따라 단순하거나 복잡하도록 테스트 작업을 사용자 정의할 수 있습니다. 예를 들어, cURL 명령을 실행하고 특정 응답을 예상할 수 있습니다. 또한 단위 테스트 스위트를 실행하거나 서드파티 서비스(예: Sauce Labs)로 기능 테스트를 실행할 수도 있습니다.

테스트로 인해 JUnit XML 형식의 결과 파일이 생성되는 경우, 결과 파일에 기반한 보고서가 각 테스트 결과 페이지의 **테스트** 탭에 표시됩니다. 테스트가 실패하면 작업도 실패합니다.

## 환경 특성(환경 변수)
{: #environment_properties}

사전정의된 환경 특성 세트를 통해 작업 실행 환경에 대한 정보에 액세스할 수 있습니다. 사전정의된 환경 특성의 전체 목록은 [환경 특성 및 리소스](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-deliverypipeline_environment)를 참조하십시오.

사용자 고유의 환경 특성을 정의할 수도 있습니다. 예를 들면, 파이프라인의 모든 스크립트에서 {{site.data.keyword.Bluemix_notm}} 리소스에 액세스하는 데 사용하는 API 키를 전달하는 `API_KEY` 특성을 정의합니다.

다음 유형의 특성을 추가할 수 있습니다.

* **텍스트**: 단일 행 값을 갖는 특성 키입니다.
* **텍스트 영역**: 다중 행 값을 갖는 특성 키입니다.
* **보안**: AES-128 암호화를 통해 보호되는 단일 행 값이 있는 특성 키입니다. 이 값은 별표로 표시됩니다.
* **특성**: 프로젝트의 저장소에 있는 파일입니다. 이 파일에는 여러 특성이 포함될 수 있습니다. 각 특성은 자체 고유의 행에 위치해야 합니다. 키-값 쌍을 구분하려면 등호 부호(=)를 사용하십시오. 모든 문자열 값을 따옴표로 묶으십시오. 예를 들어, `MY_STRING="SOME STRING VALUE"`입니다.

작업 스크립트에서 `env` 명령을 실행하여 파이프라인 작업에 대한 환경 특성을 조사할 수 있습니다.
{:tip}

### 파이프라인 특성
파이프라인 특성 페이지의 오버플로우 메뉴에서 파이프라인 특성을 정의하려면 **파이프라인 구성**을 선택하십시오.

![파이프라인 오버플로우 메뉴](images/OverflowMenu.png)

파이프라인 구성 페이지의 **환경 특성** 탭에서 파이프라인 레벨 환경 특성을 설정하십시오.

![파이프라인 특성 페이지](images/PipelineProperties.png)

### 단계 특성
단계 특성을 정의하려면 단계 구성 페이지를 열고 **환경 특성** 탭을 클릭하십시오.

![단계 특성 페이지](images/StageProperties.png)

특성을 내보내서 동일한 단계의 작업 간에 환경 특성을 전달할 수도 있습니다. 예를 들면 다음 단계 내의 다른 작업에서 `$API_KEY` 특성을 사용하려면 다음 명령을 포함할 수 있습니다. `export API_KEY=<insert API key here>`
{:tip}

### 계산된 특성
단계가 실행되는 동안 `build.properties` 파일을 작성하여 여러 단계에 걸쳐 공유되는 환경 특성 값을 계산한 후 다음 단계에서 해당 파일을 실행할 수 있습니다. 예를 들어, 빌드 작업에서는 다음 명령을 빌드 스크립트에 포함할 수 있습니다.

  `echo "IMAGE_NAME=${FULL_REPOSITORY_NAME}" >> $ARCHIVE_DIR/build.properties`

파일이 존재하는 경우 `build.properties` 파일을 실행하면 모든 작업이 시작됩니다.

## 아티팩트 작성 및 사용
{: #artifacts}

빌드 작업은 사용자 스크립트가 실행되는 현재 폴더에 컨텐츠를 자동으로 페치합니다. 나중에 배치하기 위해 전체 Git 저장소 컨텐츠가 필요하지 않은 경우 명시적 출력 디렉토리를 구성한 다음 관련 아티팩트를 해당 디렉토리에 복사 또는 작성하는 것이 좋습니다.  작업 스크립트가 빌드 결과에서 실행됩니다(출력 디렉토리).

Cloud Foundry에 배치하는 작업은 권한 작업이 실행되는 사용자의 플랫폼 API 키 및 아티팩트를 배치할 지역, 조직 및 영역을 지정해야 합니다. 앱을 실행하기 위해 추가 서비스가 필요한 경우 `manifest.yml` 파일에 지정해야 합니다.

{{site.data.keyword.containerlong_notm}}에 배치하는 배치 작업은 권한 작업이 실행되는 사용자의 플랫폼 API 키, Dockerfile 및 선택적으로 Helm 차트를 지정해야 합니다.  

지정된 플랫폼 API 키를 사용하여 작업이 대상 환경에 로그인한 후에 작업 스크립트가 실행됩니다(스크립트에서 `cf push` 또는 `kubectl` 명령을 실행할 수 있도록 함).

## 파이프라인 예
{: #deliverypipeline_example}

단순 파이프라인에는 세 개의 단계가 포함될 수 있습니다.

1. 앱에서 빌드 프로세스를 컴파일하고 실행하는 빌드 단계
2. 앱의 인스턴스를 배치한 후 거기서 테스트를 실행하는 테스트 단계
3. 테스트한 앱의 프로덕션 인스턴스를 배치하는 프로덕션 단계

다음 개념 다이어그램에 이 파이프라인이 표시되어 있습니다.

![파이프라인에 있는 단계 및 작업의 개념 다이어그램](images/diagram.jpg)

*3단계 파이프라인의 개념 모델*

단계는 저장소와 빌드 작업에서 입력을 받으며 단계 내의 작업은 순차적으로, 그리고 서로 독립적으로 실행됩니다. 파이프라인 예에서, 테스트 및 프로덕션 단계가 모두 빌드 단계의 출력을 입력으로 받지만 단계는 순차적으로 실행됩니다.

## Cloud Foundry Manifest 파일
{: #deliverypipeline_manifest}

프로젝트 루트 디렉토리에 저장되어 있는 `manifest.yml`이라는 이름의 Manifest 파일은 프로젝트가 {{site.data.keyword.Bluemix_notm}}에 배치되는 방법을 제어합니다. 프로젝트의 Manifest 파일 작성에 대한 정보는 [애플리케이션 Manifest에 대한 {{site.data.keyword.Bluemix_notm}} 문서](/docs/cloud-foundry?topic=cloud-foundry-deploy-apps#appmanifest)를 참조하십시오. {{site.data.keyword.Bluemix_notm}}와 통합하려면 프로젝트의 루트 디렉토리에 Manifest 파일이 있어야 합니다. 그러나 이 파일의 정보를 기반으로 배치하지 않아도 됩니다.

파이프라인에서 `cf push` 명령 인수를 사용하여 Manifest 파일이 할 수 있는 모든 작업을 지정할 수 있습니다. `cf push` 명령 인수는 배치 대상이 여러 개인 프로젝트에서 유용합니다. 여러 배치 작업이 모두 프로젝트 Manifest 파일에 지정된 라우트를 사용하려 하면 충돌이 발생합니다.

충돌을 피하려면 `cf push`와 그 뒤에 호스트 이름 인수 `-n` 및 라우트 이름을 사용하여 라우트를 지정하면 됩니다. 개별 단계의 배치 스크립트를 수정하면 여러 대상에 배치할 때 라우트 충돌을 피할 수 있습니다.

`cf push` 명령 인수를 사용하려면 배치 작업의 구성 설정을 열어 **배치 스크립트** 필드를 수정하십시오. 자세한 정보는 [Cloud Foundry Push 문서![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html#push){: new_window}를 참조하십시오.
