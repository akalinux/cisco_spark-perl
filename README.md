
# Current Documentation

For the full documentation, please see the perldoc(s)

## Basic Example

This example shows how to connect to spark and respond to text messages.
```
use Modern::Perl;
use Data::Dumper;
use AnyEvent::SparkBot;
use AnyEvent::Loop;
$|=1;

my $obj=new AnyEvent::SparkBot(token=>$ENV{SPARK_TOKEN},on_message=>\&cb);

$obj->que_getWsUrl(sub { $obj->start_connection});
$obj->agent->run_next;
AnyEvent::Loop::run;

sub cb {
  my ($sb,$result,$eventType,$verb,$json)=@_;
  return unless $eventType eq 'conversation.activity' and $verb eq 'post';
  if($result) {
    my $data=$result->get_data;
    my $response={
      roomId=>$data->{roomId},
      personId=>$data->{personId},
      text=>"ya.. ya ya.. I'm on it!"
    };
    print Dumper($data);
    $sb->spark->que_createMessage(sub {},$response);
    $sb->agent->run_next;
  } else {
    print "Error: $result\n";
  }
}
```

## To Build:
```
  perl MakeFile.PL
  make
  make test
  make install
```

## For more extensive unit testing

If you want to test this object with your token
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
