If you want to test this object with your token

All Formal use case documentation is contained in the perldoc and pod files.

To Build:
```
  perl MakeFile.PL
  make
  make test
  make install
```

To run the unit tests with your test info
```
  export SPARK_TOKEN=myToken
  export TEST_USER='Firstname LastName'
  export RUN_HTTP_TESTS=1
  export TEST_USER_WC='User%'
  export TEST_EMAIL='User%'
  export TEST_PERSON_ID=xxxxx
  export TEST_MSG_ID=xxx
  perl MakeFile.PL
  make
  make test
  make install
```
