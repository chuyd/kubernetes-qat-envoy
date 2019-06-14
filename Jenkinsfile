pipeline {
  agent {
    label "kubernetes-qat-envoy"
  }
  environment {
    QAT_VERSION="1.7.l.4.5.0-00034"
    QAT_SHA_256="c42a3afc1a5c76d441eaca8b97dc1f9ee64939ec001539ee1a2f3b39b7543c8e"
    REPO_URL="https://github.com/intel/kubernetes-qat-envoy"
  }
  stages {
    stage('Create container for QAT-accelerated Envoy') {
      options {
        timeout(time: 90, unit: "MINUTES")
        retry(2)
      }
      steps {
        sh "wget https://01.org/sites/default/files/downloads/qat${QAT_VERSION}.tar.gz"
        sh "sha256sum qat${QAT_VERSION}.tar.gz | grep $QAT_SHA_256"
        sh "docker image build -t envoy-qat:devel -f Dockerfile.envoy ."
      }
    }
  }
}
