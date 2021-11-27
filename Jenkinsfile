// vi:set nu ai ap aw smd showmatch tabstop=4 shiftwidth=4: 

library 'jenkins-shared-library'

pipeline {
  agent { label 'beast4' }
  options {
    timestamps();
  }

  environment {
	GIT_REPO_NAME = env.GIT_URL.replaceFirst(/^.*\/([^\/]+?).git$/, '$1')
	GIT_BRANCH_NAME = "${GIT_BRANCH.split('/').size() >1 ? GIT_BRANCH.split('/')[1..-1].join('/') : GIT_BRANCH}"
  }

  parameters {
    string(defaultValue: "tom.tsand.org", description: "Specify FQDN", name: "NODEFQDN" )
	string(defaultValue: "2048", description: "Ram size", name: "RAM" )
	string(defaultValue: "2", description: "CPU Count", name: "VCPUS" )
	string(defaultValue: "16", description: "Root Size (GB)", name: "ROOTSIZE" )
	choice(choices: '16.04 - xenial\n18.04 - bionic\n20.04 - focal', description: 'Distribution', name: "DISTRO" )
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
          sudo make -e NAME=${params.NODEFQDN} RAM=${params.RAM} VCPUS=${params.VCPUS} ROOTSIZE=${params.ROOTSIZE} DISTRO=${params.DISTRO} node
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
