// pipeline {
//     agent {
//         docker {
//             image 'node:18'
//             args '-v /var/run/docker.sock:/var/run/docker.sock'
//         }
//     }

//     environment {
//         SNYK_TOKEN = credentials('SNYK_TOKEN')
//     }

//     stages {
//         stage('Checkout Code') {
//             steps {
//                 git branch: 'main', url: 'https://github.com/your-repo.git'
//             }
//         }

//         stage('Install Dependencies') {
//             steps {
//                 sh 'npm install'
//             }
//         }

//         stage('Snyk Scan') {
//             steps {
//                 sh '''
//                 snyk auth $SNYK_TOKEN
//                 snyk test || true
//                 '''
//             }
//         }

//         stage('Build') {
//             steps {
//                 sh 'npm run build'
//             }
//         }

//         stage('Test') {
//             steps {
//                 sh 'npm test'
//             }
//         }
//     }

//     post {
//         success {
//             echo 'Pipeline completed successfully!'
//         }
//         failure {
//             echo 'Pipeline failed!'
//         }
//     }
// }


def snykCliBaseName(){
if (isUnix()) {
def uname = sh script: 'uname', returnStdout: true
if (uname.startsWith("Darwin")) {
return "snyk-macos"
} else {
return "snyk-linux"
}
} else {
return "snyk-win.exe"
}
}

node {

stage('Download Latest Snyk CLI') {
echo "Getting Snyk CLI Version"

def latest_version = GetSnykVersion()
echo "Latest Snyk CLI Version: ${latest_version}"

def snyk_cli_dl_linux=https://github.com/snyk/snyk/releases/download/${latest_version}/snyk-linux<https://github.com/snyk/snyk/releases/download/$%7blatest_version%7d/snyk-linux>
echo "Download URL: ${snyk_cli_dl_linux}"

sh """
rm -rf ./snyk
curl -Lo ./snyk "${snyk_cli_dl_linux}"
chmod +x snyk
ls -la
./snyk -v
"""
}
}