# grepyang
Greps through a [YANG](https://tools.ietf.org/html/rfc7950) module, and takes out blocks matching a key. _grepyang_ runs on _dgsh,_ [the Directed Graph Shell](https://github.com/dspinellis/dgsh).

## Usage
### Find a block within a module
```
# /grepyang cancel-commit ietf-netconf@2011-06-01.yang
853:  rpc cancel-commit {
854:    if-feature confirmed-commit;
855:    description
856:      "This operation is used to cancel an ongoing confirmed commit.
857:       If the confirmed commit is persistent, the parameter
858:       'persist-id' must be given, and it must match the value of the
859:       'persist' parameter.";
860:    reference "RFC 6241, Section 8.4.4.1";
861:
862:    input {
863:      leaf persist-id {
864:        type string;
865:        description
866:          "This parameter is given in order to cancel a persistent
867:           confirmed commit.  The value must be equal to the value
868:           given in the 'persist' parameter to the <commit> operation.
869:           If it does not match, the operation fails with an
870:          'invalid-value' error.";
871:      }
872:    }
873:  }
```

### Find a block within a block
```
# /grepyang input cancel-commit ietf-netconf@2011-06-01.yang
853:  rpc cancel-commit {
862:    input {
863:      leaf persist-id {
864:        type string;
865:        description
866:          "This parameter is given in order to cancel a persistent
867:           confirmed commit.  The value must be equal to the value
868:           given in the 'persist' parameter to the <commit> operation.
869:           If it does not match, the operation fails with an
870:          'invalid-value' error.";
871:      }
872:    }
872:    }
873:  }
```
