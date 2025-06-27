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
          snykTokenId:      'SNYK_TOKEN',

          /* common quality-gate knobs */
          failOnIssues:     true,            // default is true
          severity:         'high',          // fail if ≥ high
          monitorProjectOnBuild: true,       // create/refresh project in app.snyk.io

          /* anything you’d normally add to `snyk test` */
          additionalArguments: '--all-projects --sarif-file-output=results.sarif'
        )
      }
    }
  }

  /* Optional: always publish the HTML report Jenkins creates */
  post {
    always { archiveArtifacts artifacts: 'results.sarif', allowEmptyArchive: true }
  }
}
