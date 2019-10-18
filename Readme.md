<ol>
  <li> Download the necessary files
  <ol>
      <li> 
        Sniper simulator 7.2 <br> 
        <code> $ wget http://snipersim.org/download/b83613395338cc0e/packages/sniper-latest.tgz </code> 
      </li>
      <li>
        pin tools <br>
        <code> $ wget https://software.intel.com/sites/landingpage/pintool/downloads/pin-3.11-97998-g7ecce2dac-gcc-linux.tar.gz </code>
      </li>
    </ol>
  </li>

  <li> 
    Then install required Dependencies <br> 
    <code> $ sudo dpkg --add-architecture i386 </code> <br>
    <code> $ sudo apt-get install binutils build-essential curl git libboost-dev libbz2-dev libc6:i386 libncurses5:i386 libsqlite3-dev libstdc++6:i386 python wget zlib1g-dev </code>
  </li>

  <li> 
    Now extract sniper file into a directory. I am assuming you will extract it in <code> ~/sniper-7.2 </code> directory. <br>
    <code> $ tar xvzf sniper-latest.tgz </code> 
  </li>
  <li>
    Now extract the pintool into another directory. I am assuming you will extract it in <code> ~/pin-3.11-97998-g7ecce2dac-gcc-linux/ </code> directory. <br>
    <code> $ tar xvzf pin-3.11-97998-g7ecce2dac-gcc-linux.tar.gz </code>
  </li>

  <li> 
    Make a folder inside the <br> <code> $ mkdir -p ~/sniper-7.2/pin_kit </code>
  </li>

  <li> Copy the pin tool extracted files to <code> ~/sniper-7.2/pin_kit/ </code> directory <br> 
    <code> $ mv ~/pin-3.11-97998-g7ecce2dac-gcc-linux/* ~/sniper-7.2/pin_kit/ </code>
  </li>

  <li>
    add <code> PIN_HOME </code> variable to system path by editing <code> ~/.bashrc </code> <br>
    <code> export PIN_HOME="~/sniper-7.2/pin_kit" </code>
  </li>

  <li> 
    Modify the <code> ~/sniper-7.2/tools/pinversion.py </code> file at <code> Line 12 </code> <br>
    <code> for filebase in ( 'source/include/pin/pin_version.h', ):
    </code> <br>
    Remember the comma after the path is important. This is to treat the range as a tuple, if we do not put the comma, then the range would be compared as a array of string instead.
  </li>

  <li>
    Edit the files to put proper namespace before <code> string, cerr and endl </code>
    <br> You can just add <code> using namespace std; </code> on the files that cause error.
    <br> Or you can add <code> std:: </code> before each instance of  <code> string, cerr and endl </code>
    <br> These are the files where you need to add <code> using namespace std;</code> after the <code> #include </code> part
    <br> 
      <ul>
        <li> sift/standalone_pin3.0/globals.cc </li> 
        <li> sift/recorder/globals.cc </li>
        <li> frontend/pin-frontend/globals.cc </li>
        <li> sift/standalone_pin3.0/globals.hh </li> 
        <li> sift/recorder/globals.hh </li>
        <li> frontend/pin-frontend/globals.hh </li>
        <li> sift/standalone_pin3.0/papi.cc </li>
        <li> sift/recorder/papi.cc </li>
        <li> sift/recorder/recorder_control.cc </li>
      </ul> 
  </li>
 
  <li> 
    Now make sure you are the <code> ~/sniper-7.2 </code> directory by doing <br>
    <code>$ cd ~/sniper-7.2 </code>
  </li>
 
  <li> 
    compile the sniper simulator <br>
    <code>$ make -j12 </code> <br>
    Here I have used -j12 because of 12 cores in my computer.
  </li>
  <li> 
    To test your build, go to one of the test directory <br>
    <code>$ cd ~/sniper-7.2/test/fft </code>
  </li>
  <li>
    run the file 
    <br> <code>$ make run </code>
  </li>
</ol>
