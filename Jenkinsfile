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
    def snykBinary = snykCliBaseName()

    sh """
    rm -rf ./snyk
    ls -la
    curl --compressed https://downloads.snyk.io/cli/stable/snyk-linux-arm64 -o snyk
    chmod +x ./snyk
    echo "Troubleshooting: "
    uname -m
    uname -a
    ls -la
    ./snyk -v
    ./snyk auth
    """
}
}