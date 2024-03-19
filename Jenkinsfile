#!groovy

node {
    try {
        stage 'Checkout'
            checkout scm
            sh 'git log HEAD^..HEAD --pretty="%h %an - %s" > GIT_CHANGES'

        stage 'Deploy'
            sh 'whoami'
            switch (env.BRANCH_NAME) {
                case 'dev':
                    sh 'bash ./.deployment/dev_deploy.sh'
                    break
                case 'uat':
                    sh 'bash ./.deployment/uat_deploy.sh'
                    break
                default: 
                    echo "Deploy scripts only on dev and master"
                    break
            }
        // stage 'Publish results'
        //     slackSend color: "good", message: "Build successful: `${env.JOB_NAME}#${env.BUILD_NUMBER}` <${env.BUILD_URL}|Open in Jenkins>"
    }

    catch (err) {
        // slackSend color: "danger", message: "Build failed :face_with_head_bandage: \n`${env.JOB_NAME}#${env.BUILD_NUMBER}` <${env.BUILD_URL}|Open in Jenkins>"

        throw err
    }


}
