# installation (IGNORE, TO BE UPDATED)

## login
```
ssh -X noah-login  # note: use campus intranet because forwarding X11 is very slow on wifi
cd /hps/nobackup/research/zi/leandro/adrian  # switch to installation dir
```

## install java
```
wget https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.2_linux-x64_bin.tar.gz
tar -zxvf openjdk-11.0.2_linux-x64_bin.tar.gz
export JAVA_HOME="/hps/nobackup/research/zi/leandro/adrian/jdk-11.0.2"
```

## install cytoscape 3.9.1, required by clusterMaker2
```
wget https://github.com/cytoscape/cytoscape/releases/download/3.9.1/Cytoscape_3_9_1_unix.sh
bash Cytoscape_3_9_1_unix.sh
```


# usage
```
ssh -X codon-login  # note: use campus intranet because forwarding X11 is very slow on wifi
module load openjdk-11.0.1-gcc-9.3.0-unymjzh

MEM_IN_GB=40  # set to how many GBs you think cytoscape will use

# run cytoscape in a worker node (type yes for any authenticity of host issues)
bsub -q gui -XF -I -R "select[mem>$((MEM_IN_GB*1024))] rusage[mem=$((MEM_IN_GB*1024))]" -M$((MEM_IN_GB*1024)) -o cytoscape_gui_.o -e cytoscape_gui_.e -J cytoscape_gui /hps/nobackup/iqbal/leandro/adrian/cytoscape/cytoscape_installation/cytoscape.sh

# now cytoscape should open on your local screen and you can use it normally

# once you are done, you can close cytoscape screen, but the cluster won't recognise you are done. You can kill all cytoscape GUI jobs by running
bjobs -w | grep cytoscape_gui | awk '{print $1}' | xargs bkill
```
