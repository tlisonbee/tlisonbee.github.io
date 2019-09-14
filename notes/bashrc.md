
# .bashrc


## AWS Command Completion

```bash
# Command completion for AWS CLI
complete -C '/usr/local/bin/aws_completer' aws
```

## Java Home on MacOS

```bash
# List all Java
/usr/libexec/java_home -V

#export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_111.jdk/Contents/Home/ && export PATH=$JAVA_HOME/bin:$PATH
#export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-11.0.1+13/Contents/Home/ && export PATH=$JAVA_HOME/bin:$PATH
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk8u192-b12/Contents/Home/ && export PATH=$JAVA_HOME/bin:$PATH

#export JAVA_HOME=`/usr/libexec/java_home -v 1.8` && export PATH=$JAVA_HOME/bin:$PATH
#export JAVA_HOME=`/usr/libexec/java_home -v 1.7` && export PATH=$JAVA_HOME/bin:$PATH
```
