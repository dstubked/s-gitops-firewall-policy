node {
    def app

    stage('Clone repository') {
        /* Clone repository to our workspace */

        checkout scm
    }
    
    stage ('Deploy Policy') {
        /* Deploy firewall policy */
        withCredentials([usernameColonPassword(credentialsId: 'aquaui', variable: 'aquauipass')]) {
            sh "curl -H 'Content-Type: application/json' -X PUT -u $aquauipass -d @Default-block-IP-list.json http://demo1985-vm0.aquaseclabs.com/api/v2/firewall_policies/EMA-Blocked-List"
        }
    }
    stage ('Validate Policy') {
        /* Get firewall policy */
        withCredentials([usernameColonPassword(credentialsId: 'aquaui', variable: 'aquauipass')]) {
            sh "curl -H 'Content-Type: application/json' -X GET -u $aquauipass http://demo1985-vm0.aquaseclabs.com/api/v2/firewall_policies/EMA-Blocked-List | jq"
        }
    }    
}
