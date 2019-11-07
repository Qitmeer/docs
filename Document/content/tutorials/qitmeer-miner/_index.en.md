# <font color=Chocolate size=6>Mining Tutorial</font>

##  Step 1: Prepare Enviroment
- Windows 10
  
  - **install opencl sdk**:
    
    N card recommend cuda v10.1 see [here](https://developer.nvidia.com/cuda-downloads) .
    
    A card recommend Official driver
                 
  - **Build Tools for Visual Studio**:  
    https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=BuildTools&rel=16

- Ubuntu 19 

   - need graph card driver
    
```bash
$ sudo apt-get install beignet-dev nvidia-cuda-dev nvidia-cuda-toolkit 
```        
 
    
## Step 2: Run Miner

- Download miner from the release [here](https://github.com/Qitmeer/qitmeer-miner/releases/tag/v0.2.4)

- Unzip the file

- Run with config file `qitmeer.conf`

    - modify the config params 
        
        - `mineraddress`=TmRvuqtjb3DsYQJTcEZQZD5qfJWcMggdEYP
        - `rpcserver`=127.0.0.1:1234
        - `rpcuser`=test
        - `rpcpass`=test      

    
    - open `cmd` tools
    
    - cd miner directory
    
```bash
# run
$ cd (miner directory)
$ ./qitmeer-miner
```
![dir](https://github.com/Qitmeer/qitmeer-docker-test/blob/master/images/miner.png)   
- Run with solo command line
    
```bash
#run 
$ cd (miner directory)
$ ./qitmeer-miner -s 127.0.0.1:1234 -u test -P test --symbol PMEER --notls -i 24 -W 256 --mineraddress RmN4SADy42FKmN8ARKieX9iHh9icptdgYNn 
```

### Param Description 
          
- `--dag` the node is dag node
- `-s` the node rpc listen address
- `-u` the node rpc username
- `-P` the node rpc password
- `--symbol` now just `MEER` is supported
- `--i` Intensities (the work size is 2^intensity) up to device
- `--W` The explicitly declared sizes of the work to do up to device (overrides intensity)
- `--mineraddress` the miner address
- `-o` the pool address
- `-m` the pool user account address
- `--notls` disable TLS for the RPC server
