pipeline {
  agent any

  /* Makes the Snyk CLI that Jenkins installed available on PATH */
  tools { snyk 'SnykLatest' }

  /* Best practice: fetch the token through Credentials Binding */
  environment {
      SNYK_TOKEN = credentials('SNYK_TOKEN_ID')
  }

  stages {
    stage('Checkout')  { steps { checkout scm } }
    stage('Build')     { steps { sh 'npm ci' } }

    stage('Snyk Open-Source Scan') {
      steps {
        snykSecurity(
          /* only these two are really required */
          snykInstallation: 'SnykLatest',
          snykTokenId:      'SNYK_TOKEN_ID',

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
