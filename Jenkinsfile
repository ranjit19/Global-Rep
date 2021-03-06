import jenkins.model.*

def GITURL = 'https://github.com/ranjit19/Global-Rep'
def BRANCH = 'main'
def PIPELINE_GITURL = 'https://github.com/ranjit19/Global-Rep'
def PACKAGE = '''$REST_SIMPLE'''
def COVERAGE = 80
def VARIANT = "DEFAULT"

parallel (
    "NPL":{
        node {
        	def LABEL = "NPL"
        	def HOST = "solmanhana.openstack.na-us-1.cloud.sap"
        	def CREDENTIAL = "NPL"
        	
        	git poll: true, branch: BRANCH, url: GITURL
        		
        	stage('[' + LABEL + '] Preparation') {
        		deleteDir()
        		dir('sap-pipeline') {
        			bat "git clone " + PIPELINE_GITURL + " ."
        		}
        	}
        	
        	def sap_pipeline = load "sap-pipeline/sap.groovy"
        	sap_pipeline.abap_unit(LABEL,HOST,CREDENTIAL,PACKAGE,COVERAGE)
        	sap_pipeline.abap_sci(LABEL,HOST,CREDENTIAL,PACKAGE,VARIANT)
        	sap_pipeline.sap_api_test(LABEL,HOST,CREDENTIAL)
        }
    }
    /* Add more system as needed...
	,"NPL":{
        node {
        	def LABEL = "NPL"
        	def HOST = "vhcalnplci.dummy.nodomain"
        	def CREDENTIAL = "NPL"
        	
        	git poll: true, branch: BRANCH, url: GITURL
        		
        	stage('[' + LABEL + '] Preparation') {
        		deleteDir()
        		dir('sap-pipeline') {
        			bat "git clone " + PIPELINE_GITURL + " ."
        		}
        	}
        	
        	def sap_pipeline = load "sap-pipeline/sap.groovy"
        	sap_pipeline.abap_unit(LABEL,HOST,CREDENTIAL,PACKAGE,COVERAGE)
        	sap_pipeline.abap_sci(LABEL,HOST,CREDENTIAL,PACKAGE,VARIANT)
        	sap_pipeline.sap_api_test(LABEL,HOST,CREDENTIAL)
        }
	} */
)
