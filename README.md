# LeagueIR NEC IR CCode Transmitter


This is a demonstration PXT project that you can use as a template for
building Micro:bit extensions. 

## Custom Docker Build Environment

This project includes a custom Docker container to replace the deprecated `pext/yotta` image used for building native MicroBit extensions. The container setup is located in the `docker/` directory.

### Docker Container Features

- **Ubuntu 20.04** base image for better yotta compatibility
- **Yotta 0.20.5** build system properly installed
- **Complete development environment** including Python 3, git, build tools
- **Dedicated build user** with appropriate permissions

### Building the Custom Container

To build the custom yotta Docker container:

```bash
cd docker
make build
```

The container is configured in `pxtarget.json` to be used automatically by PXT when building native code extensions.

## Getting started

If you don't have npm locally, install it. 

After cloning the repo, run `make setup` to install `pxt`, and the microbit target. 

Then you can run `make build` to build the target. Note that the compiler is
running remotely, via a web request, so you may see a lot of 'Polling ...'
messages if the build server is slow.

If you microbit is plugged in and mounted at the standard place (
`/Volumes/MICROBIT` on a Mac) then `make deploy` will deploy the code. 

### Running MakeCode Locally

You can run makecode locally using `pxt serve`, but apparently only from the pxt-microbit source
directory. Here are the instructions: 

https://github.com/microsoft/pxt-microbit/tree/master?tab=readme-ov-file#local-server-setup

This involved going to a new directory ( probably parallel to your microbit project ), then:

```bash
git clone https://github.com/microsoft/pxt-microbit
cd pxt-microbit
install -g pxt
npm install
pxt serve
```

## Docker Build Environment

### Available Docker Commands

- `make build` - Build the Docker image
- `make rebuild` - Build with no cache (force rebuild)
- `make push` - Push image to registry (requires login)
- `make clean` - Remove the Docker image locally
- `make info` - Show image information
- `make test` - Test the container
- `make help` - Show help message

### Custom Build Configuration

The project uses a custom `pxtarget.json` configuration that specifies:
- **Docker image**: `leaguepulse/yotta:latest`
- **Build engine**: `yotta`
- **Target**: `bbc-microbit-classic-gcc-nosd`

This replaces the deprecated `pext/yotta` image and provides a stable, maintainable build environment for MicroBit extensions.