#### blitz
1. no compilation on this side, but it applies the required libraries into their directories so that a command like ros2 launch or ros2 run knows where exactly to look for these files
2. the ros2 share directory line makes sure ros2 can find its non executable assets primarily your launch files, just for configuration on what all has to run not directly running noes
3. the ros2 lib line makes sure these packages are labelled as executables and dropped in the "library" so ros2 knows where to pickup if you run ros2 run blitz packer.py


#### robot interfaces 
1. checks the availability of all the dependencies as defined in the package.xml, then passes all the listed files to be converted into c++, py classes
2. flags the particular msg so when a node asks for a .msg it knows where to find