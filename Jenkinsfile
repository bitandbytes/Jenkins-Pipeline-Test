String Branch = "BF74"
String ProcessChoices = ["None", "Debug", "Release", "Debug and Release", "Release and Publish", "All"].join("\n")

def Test(String Workspace, String Branch) {
   echo "TEST ${Workspace} ${Branch}"
}

def Build(String Workspace, String Branch, String Product, String Mode) {
   echo "BUILD ${Workspace} ${Branch} ${Product} ${Mode}"
}

def Publish(String Workspace, String Branch, String Product) {
   echo "PUBLISH ${Workspace} ${Branch} ${Product}"
}

pipeline {
   agent any

      environment {
       DebugPattern = "Debug|Debug and Release|All"
       ReleasePattern = "Release|Debug and Release|Release and Publish|Release and Test|All"
       TestPattern = "Release and Test|All"
       PublishPattern = "Release and Publish|All"
   }

   parameters {
       choice(name: 'Process', choices: ProcessChoices)
   }

   stages {
       stage ('build base') {
           when { expression { params.Process.matches(env.ReleasePattern)}}
           steps { Build(Workspace, Branch, "Products.Base", "Modes.Release")}
       }

       stage ('parallel') {
           parallel {
               stage ("test base") { 
                   when { expression { params.Process.matches(env.TestPattern)}} 
                   steps { Test(WORKSPACE, env.Branch) }
               } 
               stage ("process products") { steps { script {
                   //A has no dependencies
                   if (params.Process.matches(env.DebugPattern))    Build(WORKSPACE, Branch, "Products.A", "Modes.Debug")
                   if (params.Process.matches(env.ReleasePattern))  Build(WORKSPACE, Branch, "Products.A", "Modes.Release")
                   if (params.Process.matches(env.PublishPattern))  Publish(WORKSPACE, Branch, "Products.A")
                   //B requires A
                   if (params.Process.matches(env.DebugPattern))    Build(WORKSPACE, Branch, "Products.B", "Modes.Debug")
                   if (params.Process.matches(env.ReleasePattern))  Build(WORKSPACE, Branch, "Products.B", "Modes.Release")
                   if (params.Process.matches(env.PublishPattern))  Publish(WORKSPACE, Branch, "Products.B")
                   //C requires B
                   if (params.Process.matches(env.DebugPattern))    Build(WORKSPACE, Branch, "Products.C", "Modes.Debug")
                   if (params.Process.matches(env.ReleasePattern))  Build(WORKSPACE, Branch, "Products.C", "Modes.Release")
                   if (params.Process.matches(env.PublishPattern))  Publish(WORKSPACE, Branch, "Products.C")

               }}}
           } 
       }
   }
}
