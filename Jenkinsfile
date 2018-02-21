#!/usr/bin/env groovy

node('master') {
         def location = ".\\RelativityAgent1\\RelativityAgent.sln"
		 def Msbuildlocation = "\"C:/Program Files (x86)/Microsoft Visual Studio/2017/Professional/MSBuild/15.0/Bin/MSBuild.exe"
		 
        
        stage('Stage Checkout') {
                checkout([$class: 'GitSCM', 
                branches: [[name: '*/master']], 
                doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], 
                userRemoteConfigs: [[url: 'https://github.com/relativitydev/agent-testable-code-fest2017.git']]])
				bat 'echo checkout complete'
        }
		
		bat 'echo before utilites'
		def	utilites = load ("Utilities.groovy")
		bat 'echo after utilites'
		
        stage('Stage build'){
                fileExists location
				bat 'S:/nuget.exe restore RelativityAgent1\\RelativityAgent.sln'
				bat 'echo nuget complete'
				bat 'echo build command starting'
				echo location
			    utilites.build_solution(Msbuildlocation)
			    bat 'echo build command done'
        }
		stage('Stage Test'){
				utilites.run_nunit3_tests()
       }
}
	   
	   
