pipeline {
    agent { docker 'ruby' }




    stages {
        stage('Setup') {
                  steps {
                    sh '''
                     cp config/database.yml.example config/database.yml
                     bundle install
                     rake db:create
                     rake db:schema:load
                     rake db:test:prepare
                     rake ci:setup:rspec spec RAILS_ENV=test
                    '''

                  }
                }

        stage('build') {
            steps {
                sh 'ruby --version'
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
                sh 'rspec'
            }
        }
    }
    post {
            always {
                echo 'This will always run'
            }
            success {
                echo 'This will run only if successful'
            }
            failure {
                echo 'This will run only if failed'
            }
            unstable {
                echo 'This will run only if the run was marked as unstable'
            }
            changed {
                echo 'This will run only if the state of the Pipeline has changed'
                echo 'For example, if the Pipeline was previously failing but is now successful'
            }
        }
}