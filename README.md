# grepyang
Greps through a [YANG](https://tools.ietf.org/html/rfc7950) module, and takes out
blocks matching a key.

## Find a block within a module
```
curl -s https://www.yangcatalog.org/all_modules/ietf-netconf@2024-04-16.yang -O
./grepyang cancel-commit ietf-netconf@2024-04-16.yang
928:  rpc cancel-commit {
929:    if-feature "confirmed-commit";
930:    description
931:      "This operation is used to cancel an ongoing confirmed commit.
932:       If the confirmed commit is persistent, the parameter
933:       'persist-id' must be given, and it must match the value of the
934:       'persist' parameter.";
935:    reference
936:      "RFC 6241, Section 8.4.4.1";
937:    input {
938:      leaf persist-id {
939:        type string;
940:        description
941:          "This parameter is given in order to cancel a persistent
942:           confirmed commit.  The value must be equal to the value
943:           given in the 'persist' parameter to the <commit>
944:           operation.  If it does not match, the operation fails
945:           with an 'invalid-value' error.";
946:      }
947:    }
948:  }
```

## Find a block within a block
```
./grepyang input cancel-commit ietf-netconf@2024-04-16.yang
928:  rpc cancel-commit {
937:    input {
938:      leaf persist-id {
939:        type string;
940:        description
941:          "This parameter is given in order to cancel a persistent
942:           confirmed commit.  The value must be equal to the value
943:           given in the 'persist' parameter to the <commit>
944:           operation.  If it does not match, the operation fails
945:           with an 'invalid-value' error.";
946:      }
947:    }
948:  }
```
