pipeline {
  agent any
  stages {
    stage('install_machine') {
      parallel {
        stage('install_machine') {
          steps {
            sh 'python2.7 /var/tmp/Nightswatch/deploy/upgrade_machines_sa.py -p $target_cluster --ininame \'/var/lib/jenkins/nightswatch/5.1/config.ini\''
          }
        }
        stage('i-frame manifest') {
          agent {
            node {
              label '133'
            }

          }
          environment {
            target_cluster = '10.65.173.133'
          }
          steps {
            build(job: 'test_iframe_manifest_npvr_5.1', quietPeriod: 1)
          }
        }
      }
    }
    stage('copy result xml') {
      steps {
        sh 'scp -p root@$target_cluster:/tmp/Iframe_manifest/*.xml .'
      }
    }
  }
  environment {
    target_cluster = '10.65.173.133'
  }
}