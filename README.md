## Daryna Aloff
## CSC 4980 | Blockchain & Applications | Assignment 4
### Description
This program creates a 'Courses' smart contract that provides functions to create course instructors and then retrieve their information via helper functions

### Prerequisites
* Please make sure you have the following components installed, in order to run this program:
    * [Node.js | npm](https://www.npmjs.com/get-npm)
        * *`npm`* is used to install components below
    * [Solidity](https://www.npmjs.com/package/solc)
    * [Truffle](https://www.npmjs.com/package/truffle)
* To verify that components have installed correctly, please run *`truffle version`* that will produce something like this:
```sh
> truffle version
Truffle v5.0.7 (core: 5.0.7)
Solidity v0.5.0 (solc-js)
Node v11.11.0
```
-------
### Changes from Solidity 0.4.18 to 0.5.0
While the guide uses an older version of Solidity (0.4.18), the Courses contract code has been slightly modified to make it compatible with version 0.5.0

-------
### Function Testing
```sh
> truffle compile
> truffle develop
> migrate --reset

# fetch and set an array of available accounts
> let accounts = await web3.eth.getAccounts()

# create an instance of Courses contract
> let courses = await Courses.new()

# verify that courses have no instructors (yet!)
> courses.countInstructors().then(count => count.toNumber())
0

# add a few instructors to the courses
> courses.setInstructor(accounts[0], 28, 'Sam', 'Adams')
> courses.setInstructor(accounts[1], 53, 'Amy', 'Smith')

# check instructors count now - we should get 2
> courses.countInstructors().then(count => count.toNumber())
2

# get addresses of all course instructors
> courses.getInstructors()
[ '0xF550aEdd8a3caDDe34d2288BaC9b7c2825815b66',
  '0x01564193704B9d04198e37e165EA31233EB5CE34' ]

# get instructor by address '0xF550aEdd8a3caDDe34d2288BaC9b7c2825815b66'
> courses.getInstructor('0xF550aEdd8a3caDDe34d2288BaC9b7c2825815b66')
Result {
  '0':
   BN {
     negative: 0,
     words: [ 28, <1 empty item> ],
     length: 1,
     red: null },
  '1': 'Sam',
  '2': 'Adams' }

# get instructor by address '0x01564193704B9d04198e37e165EA31233EB5CE34'
> courses.getInstructor('0x01564193704B9d04198e37e165EA31233EB5CE34')
Result {
  '0':
   BN {
     negative: 0,
     words: [ 53, <1 empty item> ],
     length: 1,
     red: null },
  '1': 'Amy',
  '2': 'Smith' }
