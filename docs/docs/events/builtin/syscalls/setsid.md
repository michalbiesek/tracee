
# setsid

## Intro
setsid - create a session and set the process group ID

## Description
setsid() creates a new session if the calling process is not a process group leader.
 The calling process is the leader of the new session (session leader) and the
process group leader of the new process group (PGID).

The process will become the only process in its session and the only process in
its process group.

The process will also be disassociated from its controlling terminal, if any.

If the calling process is already a process group leader, setsid() will fail with
EPERM.

## Arguments
* `pid`:`pid_t`[U] - PID of the session/process group leader to be replaced if positive, 
or to be created if 0 or negative.

### Available Tags
* K - Originated from kernel-space.
* U - Originated from user space (for example, pointer to user space memory used to get it)
* TOCTOU - Vulnerable to TOCTOU (time of check, time of use)
* OPT - Optional argument - might not always be available (passed with null value)

## Hooks
### do_setsid
#### Type
KProbes 
#### Purpose
To monitor the creation of new sessions/process groups.

## Example Use Case
For example, setsid() could be used when a process is executed through a child 
process, so that it also creates its own session.

## Issues
Setsid() is not allowed if the calling process is already a process group leader,
so other methods of creating independent process group should be used in that case.

## Related Events
* fork - to create a new process 
* setpgid - to set the process group ID of a process

> This document was automatically generated by OpenAI and needs review. It might
> not be accurate and might contain errors. The authors of Tracee recommend that
> the user reads the "events.go" source file to understand the events and their
> arguments better.