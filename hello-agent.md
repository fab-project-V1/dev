Hello, Agent!
Welcome to your first Fabric agent. This tutorial walks you through creating a minimal .fab module and executing it locally using the Fabric CLI.

🧠 What You’ll Learn
Basic structure of a Fabric agent.

Writing your first .fab file.

Running the agent in a local test environment.

🧰 Prerequisites
Fabric CLI installed (pip install fab-cli)

Docker (for local sandbox runtime)

A working directory (e.g., ~/fabric-lab)

1️⃣ Create Your Project
bash
Copy
Edit
mkdir hello-agent
cd hello-agent
fab init
This scaffolds a basic project.fab file.

2️⃣ Define a Minimal Agent
Replace the contents of project.fab with:

fab
Copy
Edit
agent HelloAgent {
  input: string
  output: string

  run {
    return "Hello, " + input + "!"
  }
}
This defines a stateless agent that appends your input to "Hello, ".

3️⃣ Compile the Agent
bash
Copy
Edit
fab build
You should see ✔ Build succeeded.

4️⃣ Run the Agent
You can now test the agent locally:

bash
Copy
Edit
fab run HelloAgent --input '"World"'
Expected output:

json
Copy
Edit
"Hello, World!"
✅ What’s Next?
Try editing the run block to:

fab
Copy
Edit
return input.uppercase()
Then rebuild and rerun to see the difference.

🧩 Summary
You’ve created a basic agent using the Fabric DSL, compiled it, and tested it interactively. This is your first step toward building complex multimodal systems in Fabric.
