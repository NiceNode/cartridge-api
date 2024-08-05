`--color never` is set to avoid reth from using non-readble charcters in the logs


```
podman run ghcr.io/paradigmxyz/op-reth node --help
Trying to pull ghcr.io/paradigmxyz/op-reth:latest...
Getting image source signatures
Copying blob sha256:907c53ec37acf33fb1fb34d3237dca01c591a651c99e65645d53fb3c87cf4b84
Copying blob sha256:4ce000a43472e4a2527834764b5044674760f1e2a766480798d03a93b51a0b39
Copying config sha256:df3def6f5116bc8c26ad6d002c3766c157cbb48273d0f014b3708970eb9f63ad
Writing manifest to image destination
Start the node

Usage: op-reth node [OPTIONS]

Options:
      --config <FILE>
          The path to the configuration file to use.

      --chain <CHAIN_OR_PATH>
          The chain this node is running.
          Possible values are either a built-in chain or the path to a chain specification file.

          Built-in chains:
              optimism, optimism-sepolia, base, base-sepolia

          [default: optimism]

      --instance <INSTANCE>
          Add a new instance of a node.

          Configures the ports of the node to avoid conflicts with the defaults. This is useful for running multiple nodes on the same machine.

          Max number of instances is 200. It is chosen in a way so that it's not possible to have port numbers that conflict with each other.

          Changes to the following port numbers: - `DISCOVERY_PORT`: default + `instance` - 1 - `AUTH_PORT`: default + `instance` * 100 - 100 - `HTTP_RPC_PORT`: default - `instance` + 1 - `WS_RPC_PORT`: default + `instance` * 2 - 2

          [default: 1]

      --with-unused-ports
          Sets all ports to unused, allowing the OS to choose random unused ports when sockets are bound.

          Mutually exclusive with `--instance`.

  -h, --help
          Print help (see a summary with '-h')

Metrics:
      --metrics <SOCKET>
          Enable Prometheus metrics.

          The metrics will be served at the given interface and port.

Datadir:
      --datadir <DATA_DIR>
          The path to the data dir for all reth files and subdirectories.

          Defaults to the OS-specific data directory:

          - Linux: `$XDG_DATA_HOME/reth/` or `$HOME/.local/share/reth/`
          - Windows: `{FOLDERID_RoamingAppData}/reth/`
          - macOS: `$HOME/Library/Application Support/reth/`

          [default: default]

      --datadir.static_files <PATH>
          The absolute path to store static files in.

Networking:
  -d, --disable-discovery
          Disable the discovery service

      --disable-dns-discovery
          Disable the DNS discovery

      --disable-discv4-discovery
          Disable Discv4 discovery

      --enable-discv5-discovery
          Enable Discv5 discovery

      --discovery.addr <DISCOVERY_ADDR>
          The UDP address to use for devp2p peer discovery version 4

          [default: 0.0.0.0]

      --discovery.port <DISCOVERY_PORT>
          The UDP port to use for devp2p peer discovery version 4

          [default: 30303]

      --discovery.v5.addr <DISCOVERY_V5_ADDR>
          The UDP IPv4 address to use for devp2p peer discovery version 5. Overwritten by `RLPx` address, if it's also IPv4

      --discovery.v5.addr.ipv6 <DISCOVERY_V5_ADDR_IPV6>
          The UDP IPv6 address to use for devp2p peer discovery version 5. Overwritten by `RLPx` address, if it's also IPv6

      --discovery.v5.port <DISCOVERY_V5_PORT>
          The UDP IPv4 port to use for devp2p peer discovery version 5. Not used unless `--addr` is IPv4, or `--discovery.v5.addr` is set

          [default: 9000]

      --discovery.v5.port.ipv6 <DISCOVERY_V5_PORT_IPV6>
          The UDP IPv6 port to use for devp2p peer discovery version 5. Not used unless `--addr` is IPv6, or `--discovery.addr.ipv6` is set

          [default: 9000]

      --discovery.v5.lookup-interval <DISCOVERY_V5_LOOKUP_INTERVAL>
          The interval in seconds at which to carry out periodic lookup queries, for the whole run of the program

          [default: 60]

      --discovery.v5.bootstrap.lookup-interval <DISCOVERY_V5_BOOTSTRAP_LOOKUP_INTERVAL>
          The interval in seconds at which to carry out boost lookup queries, for a fixed number of times, at bootstrap

          [default: 5]

      --discovery.v5.bootstrap.lookup-countdown <DISCOVERY_V5_BOOTSTRAP_LOOKUP_COUNTDOWN>
          The number of times to carry out boost lookup queries at bootstrap

          [default: 100]

      --trusted-peers <TRUSTED_PEERS>
          Comma separated enode URLs of trusted peers for P2P connections.

          --trusted-peers enode://abcd@192.168.0.1:30303

      --trusted-only
          Connect to or accept from trusted peers only

      --bootnodes <BOOTNODES>
          Comma separated enode URLs for P2P discovery bootstrap.

          Will fall back to a network-specific default if not specified.

      --dns-retries <DNS_RETRIES>
          Amount of DNS resolution requests retries to perform when peering

          [default: 0]

      --peers-file <FILE>
          The path to the known peers file. Connected peers are dumped to this file on nodes
          shutdown, and read on startup. Cannot be used with `--no-persist-peers`.

      --identity <IDENTITY>
          Custom node identity

          [default: reth/v1.0.3-390f30aa/aarch64-unknown-linux-gnu]

      --p2p-secret-key <PATH>
          Secret key to use for this node.

          This will also deterministically set the peer ID. If not specified, it will be set in the data dir for the chain being used.

      --no-persist-peers
          Do not persist peers.

      --nat <NAT>
          NAT resolution method (any|none|upnp|publicip|extip:\<IP\>)

          [default: any]

      --addr <ADDR>
          Network listening address

          [default: 0.0.0.0]

      --port <PORT>
          Network listening port

          [default: 30303]

      --max-outbound-peers <MAX_OUTBOUND_PEERS>
          Maximum number of outbound requests. default: 100

      --max-inbound-peers <MAX_INBOUND_PEERS>
          Maximum number of inbound requests. default: 30

      --pooled-tx-response-soft-limit <BYTES>
          Experimental, for usage in research. Sets the max accumulated byte size of transactions
          to pack in one response.
          Spec'd at 2MiB.

          [default: 2097152]

      --pooled-tx-pack-soft-limit <BYTES>
          Experimental, for usage in research. Sets the max accumulated byte size of transactions to
          request in one request.

          Since `RLPx` protocol version 68, the byte size of a transaction is shared as metadata in a
          transaction announcement (see `RLPx` specs). This allows a node to request a specific size
          response.

          By default, nodes request only 128 KiB worth of transactions, but should a peer request
          more, up to 2 MiB, a node will answer with more than 128 KiB.

          Default is 128 KiB.

          [default: 131072]

RPC:
      --http
          Enable the HTTP-RPC server

      --http.addr <HTTP_ADDR>
          Http server address to listen on

          [default: 127.0.0.1]

      --http.port <HTTP_PORT>
          Http server port to listen on

          [default: 8545]

      --http.api <HTTP_API>
          Rpc Modules to be configured for the HTTP server

          [possible values: admin, debug, eth, net, trace, txpool, web3, rpc, reth, ots, eth-call-bundle]

      --http.corsdomain <HTTP_CORSDOMAIN>
          Http Corsdomain to allow request from

      --ws
          Enable the WS-RPC server

      --ws.addr <WS_ADDR>
          Ws server address to listen on

          [default: 127.0.0.1]

      --ws.port <WS_PORT>
          Ws server port to listen on

          [default: 8546]

      --ws.origins <ws.origins>
          Origins from which to accept `WebSocket` requests

      --ws.api <WS_API>
          Rpc Modules to be configured for the WS server

          [possible values: admin, debug, eth, net, trace, txpool, web3, rpc, reth, ots, eth-call-bundle]

      --ipcdisable
          Disable the IPC-RPC server

      --ipcpath <IPCPATH>
          Filename for IPC socket/pipe within the datadir

          [default: /tmp/reth.ipc]

      --authrpc.addr <AUTH_ADDR>
          Auth server address to listen on

          [default: 127.0.0.1]

      --authrpc.port <AUTH_PORT>
          Auth server port to listen on

          [default: 8551]

      --authrpc.jwtsecret <PATH>
          Path to a JWT secret to use for the authenticated engine-API RPC server.

          This will enforce JWT authentication for all requests coming from the consensus layer.

          If no path is provided, a secret will be generated and stored in the datadir under `<DIR>/<CHAIN_ID>/jwt.hex`. For mainnet this would be `~/.reth/mainnet/jwt.hex` by default.

      --auth-ipc
          Enable auth engine API over IPC

      --auth-ipc.path <AUTH_IPC_PATH>
          Filename for auth IPC socket/pipe within the datadir

          [default: /tmp/reth_engine_api.ipc]

      --rpc.jwtsecret <HEX>
          Hex encoded JWT secret to authenticate the regular RPC server(s), see `--http.api` and `--ws.api`.

          This is __not__ used for the authenticated engine-API RPC server, see `--authrpc.jwtsecret`.

      --rpc.max-request-size <RPC_MAX_REQUEST_SIZE>
          Set the maximum RPC request payload size for both HTTP and WS in megabytes

          [default: 15]

      --rpc.max-response-size <RPC_MAX_RESPONSE_SIZE>
          Set the maximum RPC response payload size for both HTTP and WS in megabytes

          [default: 160]
          [aliases: rpc.returndata.limit]

      --rpc.max-subscriptions-per-connection <RPC_MAX_SUBSCRIPTIONS_PER_CONNECTION>
          Set the maximum concurrent subscriptions per connection

          [default: 1024]

      --rpc.max-connections <COUNT>
          Maximum number of RPC server connections

          [default: 500]

      --rpc.max-tracing-requests <COUNT>
          Maximum number of concurrent tracing requests

          [default: 6]

      --rpc.max-blocks-per-filter <COUNT>
          Maximum number of blocks that could be scanned per filter request. (0 = entire chain)

          [default: 100000]

      --rpc.max-logs-per-response <COUNT>
          Maximum number of logs that can be returned in a single response. (0 = no limit)

          [default: 20000]

      --rpc.gascap <GAS_CAP>
          Maximum gas limit for `eth_call` and call tracing RPC methods

          [default: 50000000]

      --rpc.eth-proof-window <RPC_ETH_PROOF_WINDOW>
          The maximum proof window for historical proof generation. This value allows for generating historical proofs up to configured number of blocks from current tip (up to `tip - window`)

          [default: 0]

      --rpc.proof-permits <COUNT>
          Maximum number of concurrent getproof requests

          [default: 25]

RPC State Cache:
      --rpc-cache.max-blocks <MAX_BLOCKS>
          Max number of blocks in cache

          [default: 5000]

      --rpc-cache.max-receipts <MAX_RECEIPTS>
          Max number receipts in cache

          [default: 2000]

      --rpc-cache.max-envs <MAX_ENVS>
          Max number of bytes for cached env data

          [default: 1000]

      --rpc-cache.max-concurrent-db-requests <MAX_CONCURRENT_DB_REQUESTS>
          Max number of concurrent database requests

          [default: 512]

Gas Price Oracle:
      --gpo.blocks <BLOCKS>
          Number of recent blocks to check for gas price

          [default: 20]

      --gpo.ignoreprice <IGNORE_PRICE>
          Gas Price below which gpo will ignore transactions

          [default: 2]

      --gpo.maxprice <MAX_PRICE>
          Maximum transaction priority fee(or gasprice before London Fork) to be recommended by gpo

          [default: 500000000000]

      --gpo.percentile <PERCENTILE>
          The percentile of gas prices to use for the estimate

          [default: 60]

TxPool:
      --txpool.pending-max-count <PENDING_MAX_COUNT>
          Max number of transaction in the pending sub-pool

          [default: 10000]

      --txpool.pending-max-size <PENDING_MAX_SIZE>
          Max size of the pending sub-pool in megabytes

          [default: 20]

      --txpool.basefee-max-count <BASEFEE_MAX_COUNT>
          Max number of transaction in the basefee sub-pool

          [default: 10000]

      --txpool.basefee-max-size <BASEFEE_MAX_SIZE>
          Max size of the basefee sub-pool in megabytes

          [default: 20]

      --txpool.queued-max-count <QUEUED_MAX_COUNT>
          Max number of transaction in the queued sub-pool

          [default: 10000]

      --txpool.queued-max-size <QUEUED_MAX_SIZE>
          Max size of the queued sub-pool in megabytes

          [default: 20]

      --txpool.max-account-slots <MAX_ACCOUNT_SLOTS>
          Max number of executable transaction slots guaranteed per account

          [default: 16]

      --txpool.pricebump <PRICE_BUMP>
          Price bump (in %) for the transaction pool underpriced check

          [default: 10]

      --blobpool.pricebump <BLOB_TRANSACTION_PRICE_BUMP>
          Price bump percentage to replace an already existing blob transaction

          [default: 100]

      --txpool.max-tx-input-bytes <MAX_TX_INPUT_BYTES>
          Max size in bytes of a single transaction allowed to enter the pool

          [default: 131072]

      --txpool.max-cached-entries <MAX_CACHED_ENTRIES>
          The maximum number of blobs to keep in the in memory blob cache

          [default: 100]

      --txpool.nolocals
          Flag to disable local transaction exemptions

      --txpool.locals <LOCALS>
          Flag to allow certain addresses as local

      --txpool.no-local-transactions-propagation
          Flag to toggle local transaction propagation

Builder:
      --builder.extradata <EXTRADATA>
          Block extra data set by the payload builder

          [default: reth/v1.0.3/linux]

      --builder.gaslimit <GAS_LIMIT>
          Target gas ceiling for built blocks

          [default: 30000000]

      --builder.interval <SECONDS>
          The interval at which the job should build a new payload after the last (in seconds)

          [default: 1]

      --builder.deadline <SECONDS>
          The deadline for when the payload builder job should resolve

          [default: 12]

      --builder.max-tasks <MAX_PAYLOAD_TASKS>
          Maximum number of tasks to spawn for building a payload

          [default: 3]

Debug:
      --debug.terminate
          Flag indicating whether the node should be terminated after the pipeline sync

      --debug.tip <TIP>
          Set the chain tip manually for testing purposes.

          NOTE: This is a temporary flag

      --debug.max-block <MAX_BLOCK>
          Runs the sync only up to the specified block

      --debug.etherscan [<ETHERSCAN_API_URL>]
          Runs a fake consensus client that advances the chain using recent block hashes on Etherscan. If specified, requires an `ETHERSCAN_API_KEY` environment variable

      --debug.rpc-consensus-ws <RPC_CONSENSUS_WS>
          Runs a fake consensus client using blocks fetched from an RPC `WebSocket` endpoint

      --debug.skip-fcu <SKIP_FCU>
          If provided, the engine will skip `n` consecutive FCUs

      --debug.skip-new-payload <SKIP_NEW_PAYLOAD>
          If provided, the engine will skip `n` consecutive new payloads

      --debug.engine-api-store <PATH>
          The path to store engine API messages at. If specified, all of the intercepted engine API messages will be written to specified location

Database:
      --db.log-level <LOG_LEVEL>
          Database logging level. Levels higher than "notice" require a debug build

          Possible values:
          - fatal:   Enables logging for critical conditions, i.e. assertion failures
          - error:   Enables logging for error conditions
          - warn:    Enables logging for warning conditions
          - notice:  Enables logging for normal but significant condition
          - verbose: Enables logging for verbose informational
          - debug:   Enables logging for debug-level messages
          - trace:   Enables logging for trace debug-level messages
          - extra:   Enables logging for extra debug-level messages

      --db.exclusive <EXCLUSIVE>
          Open environment in exclusive/monopolistic mode. Makes it possible to open a database on an NFS volume

          [possible values: true, false]

Dev testnet:
      --dev
          Start the node in dev mode

          This mode uses a local proof-of-authority consensus engine with either fixed block times
          or automatically mined blocks.
          Disables network discovery and enables local http server.
          Prefunds 20 accounts derived by mnemonic "test test test test test test test test test test
          test junk" with 10 000 ETH each.

      --dev.block-max-transactions <BLOCK_MAX_TRANSACTIONS>
          How many transactions to mine per block

      --dev.block-time <BLOCK_TIME>
          Interval between blocks.

          Parses strings using [`humantime::parse_duration`]
          --dev.block-time 12s

Pruning:
      --full
          Run full node. Only the most recent [`MINIMUM_PRUNING_DISTANCE`] block states are stored. This flag takes priority over pruning configuration in reth.toml

Rollup:
      --rollup.sequencer-http <HTTP_URL>
          HTTP endpoint for the sequencer mempool

      --rollup.disable-tx-pool-gossip
          Disable transaction pool gossip

      --rollup.enable-genesis-walkback
          Enable walkback to genesis on startup. This is useful for re-validating the existing DB prior to beginning normal syncing

      --rollup.compute-pending-block
          By default the pending block equals the latest block to save resources and not leak txs from the tx-pool, this flag enables computing of the pending block from the tx-pool instead.

          If `compute_pending_block` is not enabled, the payload builder will use the payload attributes from the latest block. Note that this flag is not yet functional.

Logging:
      --log.stdout.format <FORMAT>
          The format to use for logs written to stdout

          [default: terminal]

          Possible values:
          - json:     Represents JSON formatting for logs. This format outputs log records as JSON objects, making it suitable for structured logging
          - log-fmt:  Represents logfmt (key=value) formatting for logs. This format is concise and human-readable, typically used in command-line applications
          - terminal: Represents terminal-friendly formatting for logs

      --log.stdout.filter <FILTER>
          The filter to use for logs written to stdout

          [default: ]

      --log.file.format <FORMAT>
          The format to use for logs written to the log file

          [default: terminal]

          Possible values:
          - json:     Represents JSON formatting for logs. This format outputs log records as JSON objects, making it suitable for structured logging
          - log-fmt:  Represents logfmt (key=value) formatting for logs. This format is concise and human-readable, typically used in command-line applications
          - terminal: Represents terminal-friendly formatting for logs

      --log.file.filter <FILTER>
          The filter to use for logs written to the log file

          [default: debug]

      --log.file.directory <PATH>
          The path to put log files in

          [default: /root/.cache/reth/logs]

      --log.file.max-size <SIZE>
          The maximum size (in MB) of one log file

          [default: 200]

      --log.file.max-files <COUNT>
          The maximum amount of log files that will be stored. If set to 0, background file logging is disabled

          [default: 5]

      --log.journald
          Write logs to journald

      --log.journald.filter <FILTER>
          The filter to use for logs written to journald

          [default: error]

      --color <COLOR>
          Sets whether or not the formatter emits ANSI terminal escape codes for colors and other text formatting

          [default: always]

          Possible values:
          - always: Colors on
          - auto:   Colors on
          - never:  Colors off

Display:
  -v, --verbosity...
          Set the minimum log level.

          -v      Errors
          -vv     Warnings
          -vvv    Info
          -vvvv   Debug
          -vvvvv  Traces (warning: very verbose!)

  -q, --quiet
          Silence all log output
          ```