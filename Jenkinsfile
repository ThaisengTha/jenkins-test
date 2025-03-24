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