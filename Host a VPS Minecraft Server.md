# How to Host a VPS Minecraft Server via Advanced Internet Technologies

Hosting a [Minecraft server](https://www.vpsmalaysia.com.my/minecraft-vps-hosting/) on a Virtual Private Server via **Advanced Internet Technologies (AIT)** gives you complete root access, dedicated resources, and full administrative freedom compared to restricted shared game hosts.

The step-by-step workflow outlines how to provision, configure, and launch a Minecraft server instance on an AIT VPS environment.

---

## Step 1: Acquire and Access Your AIT VPS

1. **Choose a Plan:** Select an appropriate AIT VPS package with sufficient RAM and disk space to support your anticipated player count, mods, or plugins.
2. **Download an SSH Client:** Download and install an SSH client like **PuTTY** (if you are on Windows) or use your native terminal on macOS/Linux.
3. **Log In:** Open your terminal, enter your AIT VPS server IP address, and log in using your root username and password. *(Note: As a security measure, password characters will remain hidden as you type).*

---

## Step 2: Install Java

Minecraft requires a Java Runtime Environment (JRE) to execute. Because AIT provides full root access, you can install Java directly via the package manager.

Run the command to install the appropriate Java Development Kit (such as OpenJDK) matching your Minecraft version requirements:

```bash
yum install java-1.8.0-openjdk -y

```

*(If you are running a modern version of Minecraft, ensure you install the matching Java version, such as Java 17 or Java 21).*

---

## Step 3: Create a Dedicated Game Directory

To keep your system files organized, create a dedicated folder structure for your game data:

```bash
mkdir -p Games/Minecraft
cd Games/Minecraft

```

---

## Step 4: Download and Initialize the Minecraft Server

1. Download the official server `.jar` file (or an optimized alternative like PaperMC) using `wget`:
```bash
wget https://launcher.mojang.com/v1/objects/.../server.jar

```


*(Replace the URL with the direct link to the exact Minecraft server version jar you wish to run).*
2. **Accept the EULA:** Before the server can successfully boot, you must agree to Minecraft's End User License Agreement by creating and editing the `eula.txt` file:
```bash
echo "eula=true" > eula.txt

```



---

## Step 5: Install Screen for Background Management

To ensure your Minecraft server continues running even after you close your SSH terminal session, install **Screen**:

```bash
yum -y install screen

```

Launch a new screen session dedicated to your game:

```bash
screen -S minecraft

```

---

## Step 6: Configure Firewall and Open Port 25565

For players to connect to your VPS, the default Minecraft port (`25565`) must be explicitly opened in your firewall:

```bash
firewall-cmd --zone=public --add-port=25565/tcp --permanent
firewall-cmd --reload

```

---

## Step 7: Launch Your Server

Start your Minecraft server instance with defined memory allocation flags (adjust `-Xmx` and `-Xms` depending on your total VPS RAM allocation):

```bash
java -Xmx1024M -Xms1024M -jar server.jar nogui

```

To detach from the active screen session and keep the server running safely in the background, press **Ctrl + A**, then **Ctrl + D**. You can reattach to the console at any time by typing `screen -r minecraft`.
