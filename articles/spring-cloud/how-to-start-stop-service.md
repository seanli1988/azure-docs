

# Overview
When using Azure Spring Cloud, sometimes you may not need to keep it running all the time, and wanted to stop the instance and start later. This start and stop feature allows you to stop the instance, after stopping, the compute resources behind Azure Spring Cloud will be deallocated, the data plane services and the apps will stop running, after started, the compute resources will be allocated, the data plane services and the apps will be recovered. The instance can be started again within maximum stop time(3 months for preview), if maximum stop time is exceeded, the instance cannot be started again.

> [!NOTE]
> Currently start and stop feature is still under preview, after preview, the maximum stop time may or may not change.
> Once instance is stopped, instance can be deleted and viewed, but all update operations besides start and stop are not allowed.

# Prerequisite
- You already have an existing Azure Spring Cloud service instance
- Or following [quick start document](https://docs.microsoft.com/en-us/azure/spring-cloud/quickstart?tabs=Azure-CLI&pivots=programming-language-java) to create one

# Start and stop with CLI
Switch to the subscription your Azure Spring Cloud service instance belongs to.
```azurecli-interactive
az account set -s <subscription name>
```

## Stop a running instance
Use `az spring-cloud stop` to stop a running Azure Spring Cloud instance:
```azurecli-interactive
az spring-cloud stop --name <service instance name> --resource-group <resource group name> [--no-wait]
```

After stopped successfully, use `az spring-cloud show` to check the power state.
```json
{
    "properties": {
        "provisioningState": "Succeeded",
        [...]
        "powerState": "Stopped"
    },
    [...]
}

## Start a stopped instance
Use `az spring-cloud start` to start a running Azure Spring Cloud instance:
```azurecli-interactive
az spring-cloud start --name <service instance name> --resource-group <resource group name> [--no-wait]
```

After started successfully, use `az spring-cloud show` to check the power state.
```json
{
    "properties": {
        "provisioningState": "Succeeded",
        [...]
        "powerState": "Running"
    },
    [...]
}
```

# Start and stop with portal
Portal can also be used to start and stop Azure Spring Cloud instances.

## Stop a running instance
1. Go to Azure Spring Cloud service overview page
2. Click the `Stop` button to stop a running instance.

:::image type="content" source="./media/spring-cloud-stop-start-service/spring-cloud-stop-service.png" alt-text="Stop Azure Spring Cloud Service":::

## Start a stopped instance
1. Go to Azure Spring Cloud service overview page
2. Click the `Start` button to stop a running instance.

:::image type="content" source="./media/spring-cloud-stop-start-service/spring-cloud-start-service.png" alt-text="Start Azure Spring Cloud Service":::