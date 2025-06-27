docker { image 'snyk/snyk-cli:arm64' }


pipeline {
  agent any

  tools {
    nodejs 'node20'       // NodeJS tool you defined
    snyk   'snyk-tool-config'   // Snyk tool you already configured
  }

  stages {
    stage('Checkout')  { steps { checkout scm } }
    stage('Build')     { steps { echo "insert build commands here"} }

    stage('Snyk Open-Source Scan') {
      steps {
        snykSecurity(
          /* only these two are really required */
          snykInstallation: 'snyk-tool-config',
          snykTokenId:      '1e2382ea-fcab-4884-a75a-97e5385e87ee',
        )
      }
    }
  }

  /* Optional: always publish the HTML report Jenkins creates */
  post {
    always { archiveArtifacts artifacts: 'results.sarif', allowEmptyArchive: true }
  }
}
