pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: '13.232.37.32', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '13.232.47.48', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
     }


        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        sh "scp -i /home/ec2-user/a.pem /home/ec2-user/apache-tomcat-8.5.31/webapps/ROOT/index.jsp ec2-user@${params.tomcat_dev}:/home/ec2-user/apache-tomcat-8.5.31_prod/webapps/ROOT"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        sh "scp -i /home/ec2-user/a.pem /home/ec2-user/apache-tomcat-8.5.31/webapps/ROOT/index.jsp ec2-user@${params.tomcat_prod}:/home/ec2-user/apache-tomcat-8.5.31_prod/webapps/ROOT"
                    }
                }
            }
        }
    }
}
