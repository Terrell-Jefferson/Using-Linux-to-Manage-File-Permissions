# Using-Linux-to-Manage-File-Permissions

## Table of Contents
- [Project Description](#project-description)
- [Task 1: Check File and Directory Details](#check-file-and-directory-details)
- [Task 2: Understanding the Permissions String](#understanding-the-permissions-string)
- [Task 3: Change File Permissions](#change-file-permissions)
- [Task 4: Change File Permissions on a Hidden File](#change-file-permissions-on-a-hidden-file)
- [Task 5: Change Directory Permissions](#change-directory-permissions)
- [Summary](#summary)

---

## Project Description
In this lab, I worked with Linux file permissions to make sure that only the correct users could access or modify files in a project folder. Some permissions did not match the needs of the research team, so I reviewed the existing settings and updated them to improve security.  
This `README` outlines the steps I followed and the commands I used.

---

## Check File and Directory Details
I started by examining the permissions of all files and folders inside the `projects` directory.

<img width="870" height="698" alt="Check File and Directory Details" src="https://github.com/user-attachments/assets/0b18d321-5022-4c0e-b9a6-6c4a3a3bcb8b" />

The first line in the screenshot shows the command I typed, and the rest shows the output. I used the `ls -la` command to list everything inside the projects directory, including hidden files. The results show one folder called `drafts`, one hidden file named `.project_x.txt`, and five other project files. The 10-character string in the first column tells you the permissions for each file or directory.

---

## Understanding the Permissions String

Linux file permissions use a 10-character string. The 10-character string can be deconstructed to determine who is authorized to access the file and their specific permissions.

The characters and what they represent are as follows:
- 1st character: This character is either a d or hyphen (-) and indicates the file type. If it’s a d, it’s a directory. If it’s a hyphen (-), it’s a regular file.

- 2nd-4th characters: These characters indicate the read (r), write (w), and execute (x) permissions for the user. When one of these characters is a hyphen (-) instead, it indicates that this permission is not granted to the user.

- 5th-7th characters: These characters indicate the read (r), write (w), and execute (x) permissions for the group. When one of these characters is a hyphen (-) instead, it indicates that this permission is not granted for the group.

- 8th-10th characters: These characters indicate the read (r), write (w), and execute (x) permissions for other. This owner type consists of all other users on the system apart from the user and the group. When one of these characters is a hyphen (-) instead, that indicates that this permission is not granted for other.

For example, the file permissions for `project_t.txt` are `-rw-rw-r--`. Since the first character is a hyphen (-), this indicates that `project_t.txt` is a file, not a directory. The second, fifth, and eighth characters are all r, which indicates that user, group, and other all have read permissions. The third and sixth characters are w, which indicates that only the user and group have write permissions. No one has execute permissions for `project_t.txt`.

---

## Change File Permissions

The organization determined that other shouldn't have write access for the `project_k.txt` file, as well as group not having read or write permissions for the `project_m.txt` file. To comply with this, I referred to the file permissions that I previously returned. I determined `project_k.txt` must have the write access removed for other, and `project_m.txt` needs read removed for group.

The following code demonstrates how I used Linux commands to do this:

<img width="869" height="272" alt="Change file permissions" src="https://github.com/user-attachments/assets/ff6fd16c-7345-4ac4-9163-ef3220386b1e" />

The chmod command changes the permissions on files and directories. The first argument indicates what permissions should be changed, and the second argument specifies the file or directory. In this example, I removed write permissions from other for the `project_k.txt` file, as well as read permissions from group for the `project_m.txt` file.

---

## Change File Permissions on a Hidden File

The research team recently archived `project_x.txt`. They do not want anyone to have write access to this project, but the user and group should have read access.

The following code demonstrates how I used Linux commands to change the permissions:

<img width="872" height="205" alt="Change file permissions on a hidden file" src="https://github.com/user-attachments/assets/e57215b0-843d-43ea-9787-89d9c7bcc211" />

The first two lines of the screenshot display the commands I entered, and the other lines display the output of the second command. I know `.project_x.txt` is a hidden file because it starts with a period (.). In this example, I removed write permissions from the user and group, and added read permissions to the group. I removed write permissions from the user with `u-w`. Then, I removed write permissions from the group with `g-w`, and added read permissions to the group with `g+r`. 

---

## Change Directory Permissions

My organization only wants the researcher2 user to have access to the `drafts` directory and its contents. This means that no one other than researcher2 should have execute permissions.

The following code demonstrates how I used Linux commands to change the permissions:

<img width="868" height="208" alt="Change directory permissions" src="https://github.com/user-attachments/assets/9712d371-d14c-4b02-aee4-ff3d2a76c8fe" />

The output shows the permissions for several files and folders. Line 1 is the current directory (`projects`), line 2 is the parent directory (`home`), line 3 is the hidden file `.project_x.txt`, and line 4 is the `drafts` directory. Only researcher2 has execute permissions for this directory. Since the group still had execute access, I used `chmod` to remove it. Researcher2 already had execute permissions, so nothing needed to be added for them.

---

## Summary

I changed several file and folder permissions in the projects directory to match what my organization needed. First, I used `ls -la` to check the current permissions. Then, based on what I found, I used `chmod` to make the necessary permission changes.

---




