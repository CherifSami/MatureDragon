# Install for Ubuntu 16.04 LTS

## Install git

    sudo apt-get install git  
    mkdir git  
    git config --global user.name “alice”  
    git config --global user.email alice@mail.com  
    git config --global core.editor gedit  
    git config --global merge.tool kdiff3  
    git config --global credential.helper cache  
    git config --global push.default simple  
    git config --list  

## Clone

    git clone https://github.com/pja35/Kraken-Free-Dragon.git  

## Install compiler tools

    sudo add-apt-repository ppa:webupd8team/java
    sudo apt-get update
    sudo apt-get install oracle-java8-installer
    java -version

Make sure it is java 8 SE from oracle, and not the open-jdk. To try with the open-jdk see next.  


## Troubleshooting the OpenJDK

Try updating the gtk/jfx distribution

    [sudo apt-get install gtk+3.0]
    [sudo apt-get install libswt-gtk-3-java]
    [sudo apt-get install libswt-gtk-3-java-gcj]
    sudo apt-get install libopenjfx-jni

If the graphics cause a rune-time error, use the `-Dprism.verbose=true` flag to get information on that. To set this flag in eclipse, place it in:

    main.Main.java > Run as... > Run configurations > Arguments > VM arguments

This could point to a missing dependency. To locate the ubuntu package that contains the missing file:

    sudo apt-get install apt-file
    apt-file update 
    apt-file search <missing file>

This will tell you what `<missing package>` to install, with a `sudo apt-get install <missing package>`.

