# EthStorage

## The EthStorage V1 Trusted Setup Ceremony (13–22 Aug 2025 UTC) invites community members to generate zk‑SNARK parameters for EthStorage’s storage proofs. Participants install the p0tion CLI, authenticate with GitHub, contribute their own randomness and then clean up. The multi‑party process ensures that as long as one participant discards their secret, the resulting parameters are secure and can be safely used in EthStorage’s on‑chain verifier.

Step-by-step guide on running a node for the EthStorage V1 Trusted Setup Ceremony. I’ll outline prerequisites, installation, setup, contribution procedures, and cleanup instructions.
I’ll provide a detailed step-by-step guide on running a node for the EthStorage V1 Trusted Setup Ceremony. I’ll outline prerequisites, installation, setup, contribution procedures, and cleanup instructions.


Below is a concise, step‑by‑step guide for running a node to contribute to the **EthStorage V1 Trusted Setup Ceremony**.  These steps summarise the official instructions from EthStorage’s blog and GitHub guides.

### 1. Prepare your environment

1. **Hardware & OS** – Use a machine with at least 2 vCPUs, 4 GB RAM and 30 GB storage (a Linux or macOS system is recommended; Windows users can run **WSL2**).
2. **GitHub account** – Your account must be at least one month old with at least one public repo, follow ≥ 5 accounts and have ≥ 1 follower.  It must also allow the ceremony tool to read/write GitHub Gists.
3. **Internet connection** – Ensure stable upload speeds; timeouts from slow connections will push you out of the queue.

### 2. Install dependencies

1. **Update packages** – On a fresh Ubuntu VPS or local Linux machine, update packages and install build tools (curl, git, etc.).
2. **Install Node.js and npm** – Install Node.js v18 and npm 9.2+ (nvm is a convenient way to manage versions).  For example:

   ```sh
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
   source .bashrc
   nvm install 18
   nvm use 18
   ```

   These steps ensure the CLI works correctly.

### 3. Set up the working directory

1. In your home folder, create a temporary folder to run the ceremony and navigate into it:

   ```sh
   mkdir ~/trusted-setup-tmp && cd ~/trusted-setup-tmp
   ```

   This keeps your environment isolated.

### 4. Install the Phase 2 CLI (p0tion)

1. Install the CLI globally using npm:

   ```sh
   npm install -g @p0tion/phase2cli
   ```

   This command makes the `phase2cli` tool available system‑wide.

### 5. Authenticate with GitHub

1. Run the following command to start the authentication process:

   ```sh
   phase2cli auth
   ```
2. The CLI will display a code and prompt you to open `https://github.com/login/device` in your browser.  Paste the code and authorise **p0tion** to access your GitHub Gists.

### 6. Contribute to the ceremony

1. (Optional) On a VPS, use a `screen` session so the process continues even if your terminal disconnects:

   ```sh
   screen -S ceremony
   ```

2. Start your contribution:

   ```sh
   phase2cli contribute -c ethstorage-v1-trusted-setup-ceremony
   ```

   The CLI downloads existing data, asks you for **entropy**, adds your randomness and uploads the result.  You can either press Enter to let it generate entropy automatically or type in a random string yourself.

3. Wait for your turn – contributions are queued.  Average contribution times on the official portal are several minutes, but queues can cause delays.  If a timeout occurs, wait for the specified cooldown period before retrying.

### 7. Clean up after contribution

1. After the CLI reports success, exit any `screen` session and run:

   ```sh
   phase2cli clean
   phase2cli logout
   ```

   This clears temporary files and revokes GitHub authorisation.
2. Delete the temporary directory:

   ```sh
   rm -rf ~/trusted-setup-tmp
   ```
3. For maximum security, shut down and destroy any VPS you used.

---

Following these steps will allow your node to safely contribute randomness to the EthStorage V1 trusted setup.  Each valid contribution strengthens the ceremony and ensures secure zk‑SNARK parameters for EthStorage’s proof‑of‑storage circuits.
