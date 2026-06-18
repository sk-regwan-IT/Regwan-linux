
# Linux — What I Know and What I Did With It

10+ years working on Linux servers in production.
GE Healthcare hospital environments. Megatron fintech platform.Harrisburg University of science and technology
This is my reference — things I used daily and what they actually mean.

---

## The Basics That Matter in Production

**Kernel** — the heart of Linux. Everything talks to the kernel.
When I was troubleshooting memory issues on hospital servers,
dmesg and top were my first commands. They talk directly
to what the kernel is reporting.

**Shell** — how I talk to the system. Bash is what I lived in.
Wrote shell scripts at Megatron to automate deployments,
log rotation, and database backups. Ran them daily via cron.

**File system** — in Linux everything is a file.
Even running processes. Even hardware devices.
This clicked for me when I started working with
Kubernetes — containers are just isolated file systems
sitting on top of Linux.

**Process states** — running, sleeping, stopped, zombie.
I used ps aux during incidents to find what was
consuming CPU or hanging. Zombie processes show up
as Z in the output.

---

## Commands I Actually Used in Production

**ls -la** — first thing I run when I land on any server.
Shows me who owns what, what permissions are set,
what is hidden. Caught a misconfigured file during
a HIPAA audit using this.

**chmod** — fixing permissions was a weekly thing.
Scripts not running because someone created them
without execute permission. chmod +x fixes it.
Learned to always check this before go-live windows.

**ps aux** — my go-to during high CPU incidents.
Sort by CPU, find the process, investigate.
Used this during the memory leak diagnosis at production.

df -h — disk space. Ran this every morning on
storage servers holding DICOM imaging data.
Full disk on a hospital imaging server means
radiologists cannot work. You check this before they call you.

**top / htop** — real time view of what the system
is doing. CPU, memory, load average.
First window I open during any production incident.

---

## A Real Incident

Server running a deployment script threw permission denied
during a hospital go-live window. 30 minutes before
clinical handover.

Ran ls -la on the script. Permissions showed 644.
Needed 755. Ran chmod +x. Script ran. Go-live completed.

Added a permission check to our pre-deployment checklist
that same night. Never happened again.

Small fix. Big lesson. Always check permissions
before production deployment windows.

---

## What I Am Doing Now

Going back through all of this properly.
Not just using commands — understanding why they work.
Building this playbook as I go so nothing stays
in my head only.
