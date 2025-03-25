// Function to get the latest Snyk version
def getSnykVersion() {
    def LATEST_VERSION = sh(script: 'curl -Is "https://github.com/snyk/cli/releases/latest" | grep "^location" | sed s#.*tag/##g', returnStdout: true)
    LATEST_VERSION = LATEST_VERSION.trim()

    if (LATEST_VERSION) {
        println "Found the latest version of Snyk: ${LATEST_VERSION}"
        return "${LATEST_VERSION}"
    } else {
        return "v1.1295.4"
    }
}

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

        def latest_version = getSnykVersion()
        echo "Latest Snyk CLI Version: ${latest_version}"

        def snyk_cli_dl_linux="https://github.com/snyk/snyk/releases/download/${latest_version}/snyk-linux"
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