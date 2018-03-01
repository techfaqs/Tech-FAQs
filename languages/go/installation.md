
## Go Installation

### Ubuntu

    sudo curl -O https://storage.googleapis.com/golang/go1.6.linux-amd64.tar.gz
    sudo tar -xvf go1.6.linux-amd64.tar.gz
    sudo mv go /usr/local

Add `go` to the `PATH` variable:

    sudo gedit ~/.profile

At the end of the file add:

    export GOROOT=$HOME/go
    export PATH=$PATH:$GOROOT/bin
Save the file and exit.
Lastly, run `source ~/.profile`

### Other Linux Distro

    wget -c https://storage.googleapis.com/golang/go1.7.3.linux-amd64.tar.gz
    sudo tar -C /usr/local -xvzf go1.7.3.linux-amd64.tar.gz
 where, `-C` specifies the destination directory

Edit `~/.profile` or `~/.bash_profile` and add:
    export  PATH=$PATH:/usr/local/go/bin
Now run `source ~/.profile` or `source ~/.bash_profile` respectively.

Check the installation,
    go version


### Windows

Download and run the installer found at http://golang.org/doc/install

### OS X

Download an install the darwin binary from https://golang.org/dl/

You can also install go using the Homebrew package manager.


## Example:
    package main

    import "fmt"
    func main() {
        fmt.Println("Hello, 世界")
    }


