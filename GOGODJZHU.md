# GOGODJZHU for codereview

This repository is a personal fork of [apache/rocketmq](https://github.com/apache/rocketmq) for learning purposes. All related learning summaries and notes will be published on my personal blog [djzhu](https://gogodjzhu.com/).

# Quick Start

To run this project using the devcontainer:

1. Open the repository in [Visual Studio Code](https://code.visualstudio.com/) with the [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) installed.
2. When prompted, reopen the project in the devcontainer.
3. The development environment will be set up automatically inside the container.
4. Use the integrated terminal to build and run the project as needed.

For more details, refer to the `.devcontainer` folder and the official documentation for devcontainers.

# Running a Local RocketMQ Cluster (1 Master, 1 Slave)

This repository provides a convenient way to start a RocketMQ cluster with one master and one slave node on a single host for development and testing purposes.

## Prerequisites
- Ensure you have [Docker](https://www.docker.com/) and [Docker Compose](https://docs.docker.com/compose/) installed.
- Open the project in VS Code with the Dev Containers extension as described above.

## How to Start the Cluster

1. **Start the Dev Container**
   - Open the repository in VS Code and reopen in the devcontainer when prompted.

2. **Start the RocketMQ Cluster**
   Use the VS Code Run/Debug UI to start each component individually:
   - Open the Run/Debug panel in VS Code (usually accessed via the play icon or `Ctrl+Shift+D`).
   - Select and launch the following configurations one by one:
     - `NamesrvStartup` (starts the NameServer)
     - `BrokerStartup-a-0` (starts the master broker)
     - `BrokerStartup-a-1` (starts the slave broker)
   This approach allows you to set breakpoints and debug each component directly in the VS Code UI.

3. **Configuration**
   As you can see in `.vscode/launch.sh`, the configuration files for the brokers and nameserver are located in the `develop/` directory:
     - `develop/namesrv/conf/` (nameserver)
     - `develop/broker-a-0/conf/` (master)
     - `develop/broker-a-1/conf/` (slave)

4. **Verifying the Cluster**
   - Use the `MQAdmin:clusterList` configuration in the VS Code Run/Debug panel to verify the cluster status:
     - In VS Code, open the Run/Debug panel, select `MQAdmin:clusterList`, and run it. This will display the current status of the cluster in the debug console.
   - You can also check the logs in the `/data/**/logs` directory of each broker to see if they are running correctly.

5. **Start the Producer and Consumer**
   - Use the VS Code Run/Debug panel to start the sample producer and consumer for RocketMQ:
     - Select and run `quickstart:Producer` to start the example producer. This will send test messages to the cluster.
     - Select and run `quickstart:Consumer` to start the example consumer. This will receive messages from the cluster.
   - Both configurations are available in the Run/Debug panel and are pre-configured to use the local NameServer address (`127.0.0.1:9876`).
   - You can set breakpoints and debug the producer or consumer code as needed.

# Additional Resources
- For more RocketMQ usage examples, see the `example/` directory.
- For advanced configuration, refer to the official [RocketMQ documentation](https://rocketmq.apache.org/docs/quick-start/).