简介

本项目仓库是从 https://github.com/bitcoin/bitcoin fork而来，fork本仓库时原项目bitcoin的master分支处于Bitcoin Core的0.16.2发布版之后又提交了若干个commit的状态，master分支的具体commit号是0df9b0aed23127acd12d9ed6a008c12be47b1cd9。

本项目的dev分支是从master分支checkout出来的，开发新功能时都从dev分支checkout出新的topic branch进行开发，各个topic branch都合并到dev分支。
dev分支也会定期从 https://github.com/bitcoin/bitcoin 的master分支更新源码。

本项目的master分支不再单独从 https://github.com/bitcoin/bitcoin 的master分支更新源码，只会从dev分支合并更新代码，
master分支作为本项目的版本发布分支，始终与线上的版本是保持同步的。


部署

(一)以下操作是在Ubuntu 18.04上进行的

1.进入用户目录下，执行git clone命令下载Bitcoin源码:
git clone https://github.com/osbc/EvidenceProof.git

2.进入EvidenceProof目录，然后切换到dev分支：

  cd EvidenceProof

  git checkout -b dev origin/dev

3.编译安装安装Bitcoin

  1) 先替换/etc/apt/sources.list这份apt-get的源文件，否则在后续安装依赖包时有些依赖包会提示找不到(这一步不是必须的，如果后面能正常安装依赖包就不需要做这一步操作了)
  
     (1)原文件备份为sources.list.bak
     
     sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
     
     (2)编辑sources.list文件
     
     sudo vim /etc/apt/sources.list
     
     将原来的内容删除，新增下面文件中的内容：  
     https://github.com/osbc/EvidenceProof/blob/dev/conf/sources.list

     (3)执行下面命令更新
     
     sudo apt-get update
     
  
  2) 然后安装依赖包：  
  
      (1)安装libssl, libevent, libboost库等
      
      sudo apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils
        
      sudo apt-get install libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-program-options-dev libboost-test-dev libboost-thread-dev


      (2)通过添加仓库安装BerkeleyDB
      
      sudo apt-get install software-properties-common
      
      sudo add-apt-repository ppa:bitcoin/bitcoin
      
      sudo apt-get update
      
      sudo apt-get install libdb4.8-dev libdb4.8++-dev
      
    
      (3)安装UPnP库:
      
      sudo apt-get install libminiupnpc-dev
      
      
      (4)安装ZMQ库
      
      sudo apt-get install libzmq3-dev
      
         
      (5)安装QT5库
      
      sudo apt-get install libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler
    
    
      (6)安装二维码库
      
      sudo apt-get install libqrencode-dev

   3) 编译安装EvidenceProof
     先进入EvidenceProof目录，然后执行：  
     
     ./autogen.sh
     
     ./configure
     
     make
     
     make install
   
4.在当前用户目录下新建.bitcoin目录

5.进入.bitcoin目录，新建 bitcoin.conf 文件，然后在 bitcoin.conf 文件中新增下面文件中内容 ：
  
  https://github.com/osbc/EvidenceProof/blob/dev/conf/bitcoin.conf

6.修改bitcoin.conf文件，利用 addnode=ip 选项分别在各个服务器上的bitcoin.conf文件中加入其他节点服务器的ip

7.在每台节点服务器上执行bitcoind命令，这些服务器会自动组成区块链网络

8.在每台服务器上执行 bitcoin-cli createwallet customerwallet 命令创建账户转账用的钱包


(二)以下操作是在Centos上进行的
