#!groovy
def branch2;
properties([disableConcurrentBuilds()])

pipeline {
    agent any
    environment {
        LABEL1 = 'true1'
        LABEL2 = 'false2'
    }

    stages {
        stage("set var") {
            steps {
                script {
                    branch2=getTag();
                }
                sh "branch2='alala'"
                sh "ls -la"
                sh 'ls -la'
                sh "echo $branch2"
                sh "echo ${branch2}"
                // sh script: """
                //     branch="ololo"
                //     echo \$branch
                //     echo ${LABEL1}
                //     echo ${LABEL2}
                //     echo ${branch2}
                //     echo $branch2
                //     branch3="elele"
                //     ${branch2}="elele2"
                //     echo ${branch2}
                //     #следующее не работает
                //     echo \${branch2}
                // """
            }
        }
        // stage("read var") {
        //     steps {
        //         sh "echo ${branch2}"
        //         sh "echo $branch2"
        //         sh script: """
        //             echo ${LABEL1}
        //             echo ${LABEL2}
        //             echo ${branch2}
        //             echo $branch2
        //         """
        //     }
        // }
    }
}

def getTag() { //useless function when using maven
    script {
        GIT_COMMIT_HASH_SHORT = sh(script: "git rev-parse HEAD | cut -c1-7", returnStdout: true).trim()
        //DATE_PART =  sh(script: "date +%Y%m%d", returnStdout: true).trim()
        DATE_PART =  sh(script: "git show -s --format=%ci | cut -d ' ' -f1 | tr -d -", returnStdout: true).trim()
        ////DATE_PART = new SimpleDateFormat("YYYYMMdd-'r'HHmm").format(new Date())
        GIT_BRANCH = sh(script: "git rev-parse --abbrev-ref HEAD | cut -d / -f 2- | tr '\\/' '_'", returnStdout: true).trim()
        tagValue = "${DATE_PART}-${GIT_BRANCH}_${GIT_COMMIT_HASH_SHORT}"
    }
    return tagValue
}