// vi:set nu ai ap aw smd showmatch tabstop=4 shiftwidth=4: 

library 'jenkins-shared-library'

pipeline {
  agent { label 'beast4' }
  options {
    timestamps();
  }

  environment {
    CAUSE = "${currentBuild.getBuildCauses()[0].shortDescription}"
	GIT_REPO_NAME = env.GIT_URL.replaceFirst(/^.*\/([^\/]+?).git$/, '$1')
	GIT_BRANCH_NAME = "${GIT_BRANCH.split('/').size() >1 ? GIT_BRANCH.split('/')[1..-1].join('/') : GIT_BRANCH}"
  }

  stages {

    stage('checkout') {
      steps {
		buildDescription "repo: ${env.GIT_REPO_NAME}  branch: ${env.GIT_BRANCH_NAME}"
        checkout scm
      }
    }

    stage('build') {
      steps {
        sh """
          sudo make -e NAME=tom.tsand.org node
        """
      }
    }
  }
  post {
    always {
      step([$class: 'WsCleanup'])
    }
  }
}
