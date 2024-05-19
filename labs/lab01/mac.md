---
layout: page
title: "Lab 1 Setup: Mac OS"
categories: lab
released: true
---

## A. Setup

1.  Install [Homebrew](https://brew.sh/), a very easy to use package manager.
    To install, go to your Terminal and enter the following:

    ```sh
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

    **Note:** During the process, you may be prompted to enter a password. When
    you enter your password, *nothing* will display on the terminal, but the
    computer is actually recording your password. This is a security measure.
    Just type your password and hit enter.

    You may be prompted to hit enter again to start the installation after entering your password.

2.  Then, check to make sure brew is working properly on your system by typing:

    ```sh
    brew doctor
    ```

    You may encounter warnings like this, but you should be fine. Proceed to the
    next step.

    ![Homebrew Warnings](img/mac/homebrew_warnings.png)

3.  If you encounter a warning asking you to download Command Line Tools, you
    will need to do this. Install Command Line Tools manually by running:

    ```sh
    xcode-select --install
    ```

5.  Install the Java JDK, git and gh. You can do this by typing:

    ```sh
    brew install java
    brew install git
    brew install gh
    ```

    {% include alert.html type="info" content="
    Recent versions of Homebrew will install Java 20 or above. Any version of
    Java that is Java 17 or higher will be sufficient for the course.
    " %}

{:start="5"}
5. 
    After successfully installing Java, please run

    ```sh
    sudo ln -sfn $(brew --prefix)/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk
    ```

    and put in your password. You may not be able to see your password while
    typing (that's ok). There shouldn't be any output after running this command.


6.  Verify your git and gh installation by typing:

    ```shell
    git --version
    gh --version
    ```

    You have successfully installed git and gh if these commands return a valid version
    number and do not fail.

    Similarly, you can verify your Java installation by typing:

    ```sh
    java -version
    javac -version
    ```

    Both of these commands should succeed and show version 17. If both
    installations are good, woohoo! Skip the rest of this guide and return to the lab.

## B. Java Install Issues

If you are still having Java install issues with Homebrew after having retried
the steps and/or conferring with your TA, it might be time for a manual
install. To install Java manually, follow the steps below. If at any point,
you believe one of the steps you have done did not work, please get in
touch with your TA before proceeding.

1.  Download "x64 DMG Installer" (non-M1 Mac) or "Arm 64 DMG Installer" (M1 Mac)
    from this
    [link](https://www.oracle.com/java/technologies/downloads/#jdk17-mac)
    and run the installer with the default options.


2.  Verify that the download succeeded by typing:

    ```sh
    ls /Library/Java/JavaVirtualMachines
    ```

    Your output should include JDK 17 (`jdk-17.0.3.jdk`) or newer.

3.  The Java installation should have included a script that outputs the file
    location of the most recent JDK installed. Run the following command:

    ```sh
    /usr/libexec/java_home
    ```

    The output you get should look similar to the following, which is the
    output on my personal computer. In particular, you should see JDK 17
    (or newer) in the output:

    ```sh
    /Library/Java/JavaVirtualMachines/jdk-17.0.3.jdk/Contents/Home
    ```

4.  Now, all that remains to do is tell the system where our install folder is.
    First, run `echo $0` to determine if you are running zsh or bash. The next
    command you have to run will be slightly different depending on whether you
    are running zsh or bash.

    If you are running zsh, type the following command:

    ```sh
    echo 'export JAVA_HOME=$(/usr/libexec/java_home)' >> ~/.zprofile
    ```

    If you are running bash, type the following command:

    ```sh
    echo 'export JAVA_HOME=$(/usr/libexec/java_home)' >> ~/.bash_profile
    ```

5.  This step is important. **Completely** close out of your terminal window,
    by using <kbd>CMD+Q</kbd>.

    {% include alert.html type="warning" content="
    If you have worked with this type of stuff
    before, you may be tempted to source your zprofile or bash_profile. Do
    **NOT** be tempted; simply close out of your terminal with <kbd>CMD+Q</kbd>.
    (Did you echo into the correct file? If you source it, you won't know.)
    " %}

{:start="6"}
6.  Restart your terminal, and verify that your environment variables have been
    setup correctly by running:

    ```sh
    echo $JAVA_HOME
    ```

    The output of this command should be non-empty and include the path to your
    JDK 17+ installation

7.  Java should properly be installed! As mentioned above, you can test this
    with the commands:

    ```sh
    java -version
    javac -version
    ```

## C. Git Install Issues

If you had installation issues with Git using Homebrew, try the instructions
"Installing on macOS" at this
[link](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
Contact your TA if you are still having issues.
