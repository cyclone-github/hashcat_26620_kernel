[![Readme Card](https://github-readme-stats.vercel.app/api/pin/?username=cyclone-github&repo=hashcat_26620_kernel&theme=gruvbox)](https://github.com/cyclone-github/hashcat_26620_kernel/)

[![GitHub issues](https://img.shields.io/github/issues/cyclone-github/hashcat_26620_kernel.svg)](https://github.com/cyclone-github/hashcat_26620_kernel/issues)
[![License](https://img.shields.io/github/license/cyclone-github/hashcat_26620_kernel.svg)](LICENSE)
<!-- [![GitHub release](https://img.shields.io/github/release/cyclone-github/hashcat_26620_kernel.svg)](https://github.com/cyclone-github/hashcat_26620_kernel/releases) -->

# hashcat Metamask -m 26620 kernel
Custom hashcat kernel for new Metamask Vaults which use dynamic iterations

_This custom kernel may be superseded when hashcat releases official support for this mode_

### Compile 26620 kernel:
- cd to your `hashcat/` directory
- save `module_26620.c` to `hashcat/src/modules/`
- save `m26620-pure.cl` to `hashcat/OpenCL/`
- save `m26620.pm` to `hashcat/tools/test_modules/`
- run these commands to compile (_you must have gcc installed and be in the root hashcat directory in order to run the compile commands below_)
  - make clean
  - make

### Notes:
- To write the 26620 kernel, a 26600 kernel was modified to read a dynamic iteration rather than using a static iteration
- Kernel has been tested with hashes using various dynamic iterations from 10000 to 600000
- Credits go to the hashcat devs who wrote the original 26600 kernel

### Test hash:
Vault extraction:
```
 ----------------------------------------------------- 
|        Cyclone's Metamask Vault Hash Extractor       |
|  Use Metamask Vault Decryptor to decrypt JSON below  |
| https://github.com/cyclone-github/metamask_decryptor |
 ----------------------------------------------------- 
{"data":"IfLSl8TvaFODPfX8hzz+/ycdIrbGTxUe4QslkFHQNrep6Ow88YNN3MJQuj0/u3OBYvrNtZh5loXaOUdoqEPSm8UfM7Vo8/mg+gXPJ285PhP8qmedPUHkEhXwTFr6UvltUW09e4lRX+XxqSvFfPjRtLgkzWYiq66F+pu+gufAzFl7jDy4uIde4XhQ6u7+qyi8wnHrF7rteFaLYb6sBON4p3wAq1Hq9dFUeigAi68xWnlEzpSIPgLxR5XRWAxIWnNFb+OPRaLsDfltWrXbtDDZDEb25vHDgVAZ9kvMHo958J3IjMg3x9ozRT9xYYPCvK6dzHqa6Dm//b3uncQtT1yF3nEP02OH1qhXtAEq/9Fm0kKPfrx9zoHsxqgL7Og/NlqiKSih6miIpToRF+bfme/Ssyn/m+b+CuQJr91kF0heumWXKfchUscxFX6rHdyCi35Dt9v48fpdJEsjgkVTjb6XBXsLTiZOfHKb4GepR7r01fq7u9MHgATFLumLJ/roSNf0Zg==","iv":"ypLEYWtsRzEw9w+Qeib/5g==","keyMetadata":{"algorithm":"PBKDF2","params":{"iterations":600000}},"salt":"PCfeUVXQ5M31RQs2rLT6kF9pJRTbT0vMyXMURoJO6EE="}
 -------------------------------------------------------- 
|           hashcat -m 26620 hash (NEW format)           |
| https://github.com/cyclone-github/hashcat_26620_kernel |
 -------------------------------------------------------- 
$metamask$600000$PCfeUVXQ5M31RQs2rLT6kF9pJRTbT0vMyXMURoJO6EE=$ypLEYWtsRzEw9w+Qeib/5g==$IfLSl8TvaFODPfX8hzz+/ycdIrbGTxUe4QslkFHQNrep6Ow88YNN3MJQuj0/u3OBYvrNtZh5loXaOUdoqEPSm8UfM7Vo8/mg+gXPJ285PhP8qmedPUHkEhXwTFr6UvltUW09e4lRX+XxqSvFfPjRtLgkzWYiq66F+pu+gufAzFl7jDy4uIde4XhQ6u7+qyi8wnHrF7rteFaLYb6sBON4p3wAq1Hq9dFUeigAi68xWnlEzpSIPgLxR5XRWAxIWnNFb+OPRaLsDfltWrXbtDDZDEb25vHDgVAZ9kvMHo958J3IjMg3x9ozRT9xYYPCvK6dzHqa6Dm//b3uncQtT1yF3nEP02OH1qhXtAEq/9Fm0kKPfrx9zoHsxqgL7Og/NlqiKSih6miIpToRF+bfme/Ssyn/m+b+CuQJr91kF0heumWXKfchUscxFX6rHdyCi35Dt9v48fpdJEsjgkVTjb6XBXsLTiZOfHKb4GepR7r01fq7u9MHgATFLumLJ/roSNf0Zg==
```
Benchmark:
```
./hashcat -b -m 26620
* Device #1: NVIDIA GeForce RTX 4090, 23820/24215 MB, 128MCU
...
Speed.#1.........:    14125 H/s (63.04ms) @ Accel:16 Loops:512 Thr:512 Vec:1
```
Hashcat:
```
./hashcat -m 26620 -a 0 hash.txt wordlist.txt
...
$metamask$600000$PCfeUVXQ5M31RQs2rLT6kF9pJRTbT0vMyXMURoJO6EE=$ypLEYWtsRzEw9w+Qeib/5g==$IfLSl8TvaFODPfX8hzz+/ycdIrbGTxUe4QslkFHQNrep6Ow88YNN3MJQuj0/u3OBYvrNtZh5loXaOUdoqEPSm8UfM7Vo8/mg+gXPJ285PhP8qmedPUHkEhXwTFr6UvltUW09e4lRX+XxqSvFfPjRtLgkzWYiq66F+pu+gufAzFl7jDy4uIde4XhQ6u7+qyi8wnHrF7rteFaLYb6sBON4p3wAq1Hq9dFUeigAi68xWnlEzpSIPgLxR5XRWAxIWnNFb+OPRaLsDfltWrXbtDDZDEb25vHDgVAZ9kvMHo958J3IjMg3x9ozRT9xYYPCvK6dzHqa6Dm//b3uncQtT1yF3nEP02OH1qhXtAEq/9Fm0kKPfrx9zoHsxqgL7Og/NlqiKSih6miIpToRF+bfme/Ssyn/m+b+CuQJr91kF0heumWXKfchUscxFX6rHdyCi35Dt9v48fpdJEsjgkVTjb6XBXsLTiZOfHKb4GepR7r01fq7u9MHgATFLumLJ/roSNf0Zg==:hashcat1

Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 26620 (MetaMask Wallet (needs all data, checks AES-GCM tag))
Hash.Target......: $metamask$600000$PCfeUVXQ5M31RQs2rLT6kF9pJRTbT0vMyX...f0Zg==
Time.Started.....: Mon Nov 18 11:51:26 2024 (2 secs)
Time.Estimated...: Mon Nov 18 11:51:28 2024 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (tmp_wordlist.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:        1 H/s (0.16ms) @ Accel:320 Loops:64 Thr:32 Vec:1
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 1/1 (100.00%)
Rejected.........: 0/1 (0.00%)
Restore.Point....: 0/1 (0.00%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:599936-599999
Candidate.Engine.: Device Generator
Candidates.#1....: hashcat1 -> hashcat1
Hardware.Mon.#1..: Temp: 47c Fan:  0% Util:100% Core:2790MHz Mem:10501MHz Bus:1
```
