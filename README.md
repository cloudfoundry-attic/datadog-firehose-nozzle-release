# datadog-firehose-nozzle-release

#### This component has been moved to [DataDog/datadog-firehose-nozzle-release](https://github.com/DataDog/datadog-firehose-nozzle-release).

#### The blobstore supporting this release will be **REMOVED**(Sept 2018). Please do not use. 

This is a BOSH release for the datadog-firehose-nozzle, which transports logs
from [Loggregator](https://github.com/cloudfoundry/loggregator) to [Datadog](https://www.datadoghq.com/).

## Deploying the Nozzle

For a general guide to deploying nozzles, see [here](https://docs.cloudfoundry.org/loggregator/nozzle-tutorial.html).

This nozzle assumes you have a Cloud Foundry deployed with a UAA client for
the datadog nozzle. Configuration for the UAA client should look something
like the following.

```
uaa:
  clients:
    datadog-firehose-nozzle:
      access-token-validity: 1209600
      authorities: doppler.firehose
      authorized-grant-types: client_credentials
      override: true
      scope: doppler.firehose
      secret: datadog-password
```

Once a Datadog client is registered in UAA, you are ready to deploy the
nozzle. The instructions here assume you are using the Ruby based Bosh CLI.

First, update `bosh-lite/stub.yml` with your Datadog API key.  Note that the
`client_secret` under the `uaa` section in `properties` will need to match
whatever password you set for the UAA client above.

Once the `stub.yml` reflects all the correct credentials, generate a manifest
with:

```
./scripts/make_manifest_spiff bosh-lite/stub.yml
```

You are now ready to deploy:

```
bosh deploy
```
