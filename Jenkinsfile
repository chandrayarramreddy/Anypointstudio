//Variables Declaration

def muleversion="4.2.2"
def env="DEV"
def bussgrp="Speridian"
def uri="https://anypoint.mulesoft.com"
def worktype="MICRO"
def worker=1
//def mvnHome = tool 'Maven'

pipeline {
  agent any
     tools {
        maven 'Maven'
        }
  stages {
 
   stage('Build') {
   steps{
      // Run the maven build
    
         bat 'mvn clean test'
    
	  
	  }
	  }  
	  
    stage('Install') {
      steps {
       
         bat 'mvn clean install -DskipTests=true'
    
      }
    }
    stage('Deploy') {
	
	//Anypoint Platform Credentails
	 environment {
        ANYPOINT_CREDENTIALS = credentials('muleapi')
      }
           steps {
         bat "mvn package deploy -Dmuleversion=${muleversion} -Dusername=${ANYPOINT_CREDENTIALS_USR} -Dpassword=${ANYPOINT_CREDENTIALS_PSW} -Denv=${env} -Dbussgrp='${bussgrp}' -Duri=${uri} -Dworktype=${worktype} -Dworker=${worker} -DmuleDeploy"
   
     }   
      }
      }
  }
