pipeline {
  agent any
  stages {
    stage('run test') {
      agent any
      environment {
        target_cluster = '10.65.173.133'
        test_name = 'test_iframe_manifest_npvr.py'
      }
      steps {
        sh '''set +e

ssh root@$target_cluster -t "pytest -s /var/Nightswatch/CI_loops/CI_loop25/Iframe_manifest/$test_name" --junitxml="/tmp/Iframe_manifest/$test_name.xml"'''
      }
    }
    stage('copy result xml') {
      agent any
      environment {
        target_cluster = '10.65.173.133'
      }
      steps {
        sh 'scp -p root@$target_cluster:/tmp/Iframe_manifest/*.xml .'
      }
    }
  }
  environment {
    target_cluster = '10.65.173.133'
  }
}