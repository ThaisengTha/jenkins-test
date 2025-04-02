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
    echo "Getting Snyk CLI Version"

    sh """
    rm -rf ./snyk
    echo "Listing all files with ls"
    ls -la
    curl --compressed https://downloads.snyk.io/cli/stable/${snykBinary} -o snyk
    chmod +x ./snyk
    ls -la
    ./snyk -v
    """
}
}