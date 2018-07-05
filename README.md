![ALMA](images/beautiful.jpg)
[Image source](http://alma.asiaa.sinica.edu.tw/_img/site_multimedia/2013AOS/IMG_4017.jpg)

## Weekly report 2018/07/02~2018/07/08
#### 1. Report to iaa
* ok

#### 2. Trace carta
* read slack
* read Interface Control Document
* architecture:
  * server ----> RPC/data(protobuf encrytion) ------[uwebsocket]------> browser
  
#### 3. uWebSocket,protobuf my test
* uwebsocket: https://github.com/duidae/uWebsocket-test
* protobuf: https://github.com/duidae/protocol-buffer-example
* uwebsocket+protobuf: 

#### 4. huge data
* [intro to HDF5, Redis](https://chtseng.wordpress.com/2017/08/15/%E5%B7%A8%E9%87%8F%E8%B3%87%E6%96%99%E7%9A%84%E5%A5%BD%E5%A4%A5%E4%BC%B4hdf5-redis/)
* HDF5 https://www.hdfgroup.org/
* redis https://redis.io/

#### 5. possible architecture for reference(於瀏覽器多人協作的功能)
* slide.com
* google doc
* github(?)

## Weekly report 2018/06/25~2018/07/01
#### 1. Trace carta
* protobuf
  * Branch: mark/newArch-testProtoBuf
  * use protobuf to transmit .fits file
  * structure of .fits file?
  * [TODO] merge scripts/install_protobuf.sh to scripts/install3party.sh
  * carta/cpp/common_config.pri, testProtoBuf.pro
* entry point for protobuf, uwebsockets
  * carta/cpp
  * 學protobuf把uwebsocket整合進去
  * practice: .fits -> (protobuf encrytion) ------[uwebsocket]-----> (protobuf decryption) -> server
* difference between scrips/buildcasa.sh & Mark's script: cmake flag
  * scrips/buildcasa.sh: 多了-DUseCasacoreNamespace=1
```
cmake -DBoost_NO_BOOST_CMAKE=1 -DCASA_BUILD=1 -DBUILD_TESTING=OFF \
     -DUseCasacoreNamespace=1 \
     -DCMAKE_INSTALL_PREFIX=../../$TARGETOS -DBUILD_PYTHON=1 \
     -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 \
     -DPYTHON_LIBRARY=/usr/lib64/libpython2.7.so \
     -DWCSLIB_ROOT_DIR=$cartawork/CARTAvis-externals/ThirdParty/wcslib \
     -DCFITSIO_ROOT_DIR=$cartawork/CARTAvis-externals/ThirdParty/cfitsio \
     -DCMAKE_BUILD_TYPE=Release \
     -DCXX11=1 ..
```
#### 2. Qt related
* qmake會根據專案檔（.pro）裡面的資訊自動生成適合平台的 Makefile
* unit Test for Qt
  * http://doc.qt.io/qt-5/qttestlib-tutorial1-example.html
* [TODO]Use Qt creator to build and debug
* update Qt?

#### 3. study docker for mac
* [docker tutorial](https://github.com/twtrubiks/docker-tutorial)
* [如何安裝 Docker for Mac ?](http://oomusou.io/docker/docker-for-mac/)
* [使用 Docker 快速建立測試環境](http://oomusou.io/docker/ubuntu/)

## Weekly report 2018/06/18~2018/06/24
#### 1. Trace & build carta
* [carta builder script from Mark](https://github.com/markccchiang/CARTA-builder)
* startCarta.sh
  * ulimit: 限制shell資源, -n: 限制開啟文件數目
```
ulimit -n 2000
$CARTAWORKHOME/CARTAvis/build/cpp/desktop/CARTA --html $CARTAWORKHOME/CARTAvis/carta/html5/desktop/desktopIndex.html
```
![build](images/2018-06-23%2019-31-45.png)

* release binary
  * CARTA-0.9r-el6-el7/bin/carta.sh <- 啟動點

#### 2. read issues/pull requests
* [protobuf tester](https://github.com/CARTAvis/carta/pull/258)

## Weekly report 2018/06/11~2018/06/17

#### 1. micro web socket study
* [uWebSockets](https://github.com/uNetworking/uWebSockets)
* WebSocket implementation for c++, javascript(Node.js)
* 目前号称最高性能的websocket c++库
* [Comparison of WebSocket implementations](https://en.wikipedia.org/wiki/Comparison_of_WebSocket_implementations)
* github repo of my practice: https://github.com/duidae/nodejs-uwebsocket-example
* possible entry in CARTA? 

#### 2. build carta viewer again on CentOS
* [CARTA viewer](https://github.com/CARTAvis/carta)
* $ sudo ./CARTAvis/carta/scripts/buildcasa.sh
``` 
CMake Error at install/config.cmake:836 (message):
  WCSLIB could not be found.  Please check!
Call Stack (most recent call first):
  CMakeLists.txt:961 (casa_find)
  
  
-- Configuring incomplete, errors occurred!
See also "/home/duidae/projects/CARTA/CARTAvis-externals/ThirdParty/casa/trunk/code/build/CMakeFiles/CMakeOutput.log".
See also "/home/duidae/projects/CARTA/CARTAvis-externals/ThirdParty/casa/trunk/code/build/CMakeFiles/CMakeError.log".
make: *** No targets specified and no makefile found.  Stop.
```
* still errors in make -j2, need to check it out
```
make[3]: Entering directory `/home/duidae/projects/CARTA/CARTAvis/build/cpp/plugins/RegionCASA'
cp -f /home/duidae/projects/CARTA/CARTAvis/carta/cpp/plugins/RegionCASA/plugin.json plugin.json
g++ -c -pipe -DCARTA_RUNTIME_CHECKS=1 -O2 -fopenmp -Wall -W -std=c++0x -D_REENTRANT -fPIC -DUseCasacoreNamespace=1 -DQT_PLUGIN -DQT_GUI_LIB -DQT_CORE_LIB -I/opt/Qt/5.3/gcc_64/mkspecs/linux-g++ -I/home/duidae/projects/CARTA/CARTAvis/carta/cpp/plugins/RegionCASA -I/home/duidae/projects/CARTA/CARTAvis/carta/cpp -I/home/duidae/projects/CARTA/CARTAvis-externals/ThirdParty/casa/trunk/linux/include -I/home/duidae/projects/CARTA/CARTAvis-externals/ThirdParty/casa/trunk/linux/include/casacore -I/home/duidae/projects/CARTA/CARTAvis-externals/ThirdParty/wcslib/include -I/home/duidae/projects/CARTA/CARTAvis-externals/ThirdParty/cfitsio/include -I/home/duidae/projects/CARTA/CARTAvis/ThirdParty/imageanalysis/include -I/opt/Qt/5.3/gcc_64/include -I/opt/Qt/5.3/gcc_64/include/QtGui -I/opt/Qt/5.3/gcc_64/include/QtCore -I. -I. -o RegionCASA.o /home/duidae/projects/CARTA/CARTAvis/carta/cpp/plugins/RegionCASA/RegionCASA.cpp
In file included from /home/duidae/projects/CARTA/CARTAvis/carta/cpp/plugins/RegionCASA/RegionCASA.cpp:1:0:
/home/duidae/projects/CARTA/CARTAvis/carta/cpp/plugins/RegionCASA/RegionCASA.h:9:54: 嚴重錯誤：imageanalysis/Annotations/AnnotationBase.h：沒有此一檔案或目錄
 #include "imageanalysis/Annotations/AnnotationBase.h"
                                                      ^
編譯插斷。
make[3]: *** [RegionCASA.o] Error 1
make[3]: Leaving directory `/home/duidae/projects/CARTA/CARTAvis/build/cpp/plugins/RegionCASA'
make[2]: *** [sub-RegionCASA-make_first] Error 2
make[2]: *** Waiting for unfinished jobs....
g++ -c -pipe -DCARTA_RUNTIME_CHECKS=1 -O2 -fopenmp -Wall -W -std=c++0x -D_REENTRANT -fPIC -DUseCasacoreNamespace=1 -DQT_PLUGIN -DQT_GUI_LIB -DQT_CORE_LIB -I/opt/Qt/5.3/gcc_64/mkspecs/linux-g++ -I/home/duidae/projects/CARTA/CARTAvis/carta/cpp/plugins/ImageStatistics -I/home/duidae/projects/CARTA/CARTAvis/carta/cpp -I/home/duidae/projects/CARTA/CARTAvis-externals/ThirdParty/casa/trunk/linux/include -I/home/duidae/projects/CARTA/CARTAvis-externals/ThirdParty/casa/trunk/linux/include/casacore -I/home/duidae/projects/CARTA/CARTAvis-externals/ThirdParty/wcslib/include -I/home/duidae/projects/CARTA/CARTAvis-externals/ThirdParty/cfitsio/include -I/home/duidae/projects/CARTA/CARTAvis/ThirdParty/imageanalysis/include -I/opt/Qt/5.3/gcc_64/include -I/opt/Qt/5.3/gcc_64/include/QtGui -I/opt/Qt/5.3/gcc_64/include/QtCore -I. -I. -o StatisticsCASARegion.o /home/duidae/projects/CARTA/CARTAvis/carta/cpp/plugins/ImageStatistics/StatisticsCASARegion.cpp
/home/duidae/projects/CARTA/CARTAvis/carta/cpp/plugins/ImageStatistics/StatisticsCASARegion.cpp:4:62: 嚴重錯誤：imageanalysis/ImageAnalysis/ImageStatsCalculator.h：沒有此一檔案或目錄
 #include "imageanalysis/ImageAnalysis/ImageStatsCalculator.h"
                                                              ^
編譯插斷。
make[3]: *** [StatisticsCASARegion.o] Error 1
make[3]: *** Waiting for unfinished jobs....
make[3]: Leaving directory `/home/duidae/projects/CARTA/CARTAvis/build/cpp/plugins/ImageStatistics'
make[2]: *** [sub-ImageStatistics-make_first] Error 2
make[2]: Leaving directory `/home/duidae/projects/CARTA/CARTAvis/build/cpp/plugins'
make[1]: *** [sub-plugins-make_first] Error 2
make[1]: Leaving directory `/home/duidae/projects/CARTA/CARTAvis/build/cpp'
make: *** [sub-cpp-make_first] Error 2
```

#### 3. computer change to MacbookPro
* ok

#### 4. study CASA
* [CASA](https://casa.nrao.edu/)
* running on Redhat 6/7 & Mac OS X
* difference between Redhat/CentOS: CentOS is a community-developed and supported alternative to RHEL(Red Hat Enterprise Linux). It is similar to Red Hat Enterprise Linux but lacks the enterprise-level support. CentOS is more or less a free replacement for RHEL with few minor configuration differences.
* [TODO] build on RHEL

#### 5. install CentOS, RHEL for practice
* ok
* RHEL needs $$, ALMA Taiwan ARC uses CentOS 7.2(ALMA T1~T7)
![centos](images/centos+RHEL.png)

## Weekly report 2018/06/04~2018/06/10

#### 0. webpage for working progress
* ok
* [webpage](https://duidae.github.io/Asiaa-work/)

#### 1. Google protocol buffers study
* smaller, faster, binary message structure like json
* protocol buffers: [https://developers.google.com/protocol-buffers/](https://developers.google.com/protocol-buffers/)
* [Overview](https://developers.google.com/protocol-buffers/docs/overview), [Tutorials](https://developers.google.com/protocol-buffers/docs/tutorials), [Github](https://github.com/google/protobuf/releases)
* protobuf install: https://github.com/google/protobuf/blob/master/src/README.md
* .proto defines message strucuture, compiler generates corresponding .h .cc file
* github repo of my practice: [cpp only(modified makefile)](https://github.com/duidae/Asiaa-work/tree/master/protobuf-example)
* possible entry in CARTA? our protobuf message structure?
* good solution for large size json needed encryption

#### 2. qt creator installation 
* ok
![qt creator](images/2018-06-09%2019-03-55%20qtcreator.png)

#### 3. preparation for report on 7/2
* computer discuss with Mark, spec ok
* necessary materials for Vicky in advance, ok

#### 4. docker study
* docker cookbook, O'reilly
![qt creator](images/docker.jpg)

#### 5. DevOps
* really helpful article...[github, CircleCI, docker](http://blog.amowu.com/2015/04/devops-continuous-integration-delivery-docker-circleci-aws-beanstalk.html)
![devop sequence diagram](images/sequence-diagram.png)

#### 5. how to do open source development/run open source project
* [Innovation Happens Elsewhere (Version 1.0)](https://www.dreamsongs.com/IHE/)

## Pull request
* [Fix] typo/delete/modify in /home/duidae/projects/CARTA/CARTAvis/carta/scripts/buildcasa.sh // 整理buildcasa.sh
    * typo: 3 ## TODO: remove installinging
    * delete: 77     #### install Qt 4.8.5
    * delete: 78     # sudo yum -y install qt-devel.x86_64
    * delete: 79     # alias qmake='qmake-qt4'
    * remove commented code
    * comment註明路徑(casa, casacore)
    * 282 cd ../../code  //是否改成cd $casawork/trunk/code 較易讀
* [Fix] carta/readme.txt -> carta/readme.md // change readme.txt to markdown
* 整理 scripts/carta.sh 
* [Fix] scripts/carta.sh
  * 53     $dirname/setupcartavis.sh 2>&1  > /dev/null  //should be >/dev/null 2>&1

## CARTA team
* Slack: https://cartaviewer.slack.com/messages/C2S1R8V9P/
* Trello: https://trello.com/b/fViU1U7v/carta-working-group

## Reference
* [ALMA](http://www.almaobservatory.org/en/home/)
* [ALMA @ Asiaa](http://alma.asiaa.sinica.edu.tw/index.php)
  * [Fix]deadlink http://almat3.asiaa.sinica.edu.tw/ganglia/
  * Interesting & beautiful, rock band?!! http://alma.asiaa.sinica.edu.tw/intro_multimedia.php
  * AcidMan: ALMA https://www.youtube.com/watch?v=ylEDfirYJaY
* [ALMA kids](http://kids.alma.cl/?lang=zh)
* [ALMA sounds(art)](http://www.almasounds.org/)
* 譬喻：從墾丁看到台北101頂端的一隻金龜子
* [CASA](https://casa.nrao.edu/)
* [Code NASA](https://code.nasa.gov/)
* [Data NASA](https://data.nasa.gov/)
* markdown syntax: [mastering markdown](https://guides.github.com/features/mastering-markdown/), [chinese](https://github.com/othree/markdown-syntax-zhtw)

## Open source
* [用Open Source工具開發軟體](http://www.study-area.org/cyril/opentools/opentools/book1.html)
* [Innovation Happens Elsewhere (Version 1.0)](https://www.dreamsongs.com/IHE/)

## [TODO]
* license study

## Questions
* why not open source CASA directly?
