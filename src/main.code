package main

import (
	"flag"
	"fmt"
	"os"
	"os/exec"
)

func main() {
	flag.Parse()

	if flag.Arg(0) == "build" {
		build()
	}
	if flag.Arg(0) == "new-app"{
		newApp()
	}
}
func newApp(){
	name := flag.Arg(1)
	fmt.Println("Creating new app..",name)
	exec.Command("git","clone","http://github.com/realprosl/dom").Run()
	os.Rename("./dom","./" + name)
	os.Chdir("./" + name )
	code := exec.Command("code",".").Run()
	if code != nil {fmt.Println(code)}
}
func build(){

	fmt.Println("Building...")

	dir := flag.Arg(1)
	pathRead := "./src/"
	pathWrite := "./" + dir + "/src/"

	os.Mkdir(dir,os.FileMode(0755))
	os.Mkdir(pathWrite,os.FileMode(0755))

	files,readDir:= os.ReadDir(pathRead)
	if readDir != nil{
		fmt.Println(readDir)
	}

	for _, f := range files {
		content ,read := os.ReadFile(pathRead + f.Name())
		if read != nil {
			fmt.Println("read:",read)
		}
		file,create := os.Create(pathWrite + f.Name())
		if create != nil {
			fmt.Println("create:",create)
		}
		file.WriteString(string(content))
	}
	runBuild := exec.Command("go","build" ,"-ldflags","-H windowsgui","main.go").Run()
	if runBuild != nil {
		fmt.Println(runBuild)
	}
	os.Rename("./main.exe","./"+dir + "/" + dir + ".exe")
}
