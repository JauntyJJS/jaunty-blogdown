---
title: "Using Docker To Setup LINEX and MoSBi in Windows 10"
subtitle: ""
excerpt: "This post aims to provide a step by step pictorial guide on how to [Docker](https://www.docker.com/) 🐳 to set up two open source web applications 🌐,
Lipid Network EXplorer ([LINEX](https://exbio.wzw.tum.de/linex/)) and Molecular Signatures with Biclustering ([MoSBi](https://exbio.wzw.tum.de/mosbi/)) in Windows 10"
date: 2022-05-31
author: "Jeremy Selva"
draft: true
images:
series:
tags:
categories:
layout: single-sidebar
editor_options: 
  chunk_output_type: console
bibliography: utils/bibliography.bib
csl: utils/f1000research.csl
---

## Introduction

[Docker](https://www.docker.com/) 🐳 has been gaining in popularity in the academic field to ensure scripts that are used to run on research data can be easily opened and explored by others. A picture friendly introduction of Docker can be found in this [Devopedia webpage](https://devopedia.org/docker).

As someone who has just started to learn how to use this in a non-computing academic lab, the onboarding learning curve for Docker just to reproduce other people works is already quite a challenge for me 😅.

In this blog, I will try to share what I have learnt by providing a step by step walk-through with pictures to show on how to install Docker 🐳 in Windows 10 and use it recreate two lipidomics software web service 🌐, one made using [Django](https://www.djangoproject.com/) called [LINEX](https://exbio.wzw.tum.de/linex/) (1), (2) and the the other using [Shiny](https://shiny.rstudio.com/) called [MoSBi](https://exbio.wzw.tum.de/mosbi/) (3). Both software are from [LpiTUM](https://www.lipitum.de/Home). I pick these two software because the end results is tangible and do not take too long to build using Docker (once it is successfully installed).

Hope that this is helpful for those who just want to use Docker 🐳 to reproduce an open source web application 🌐.

Do note that I am using the Windows Subsystem for Linux (WSL) 2 back end approach to install Docker 🐳.

## About LINEX

[LINEX](https://exbio.wzw.tum.de/linex/) or Lipid Network EXplorer is one of the many lipidomics software used to analyse and visualise lipid metabolic networks. This is essential in helping us better understand functional association between lipids. As a result, it provides a more reliable biological interpretation of a given lipidomics experiment.

While there is a [web service](https://exbio.wzw.tum.de/linex/) available, LINEX also offers a different approach by running it in a [Docker](https://www.docker.com/) environment as well. A short instruction is provided in their [GitLab website](https://gitlab.lrz.de/lipitum-projects/linex).

## About MoSBi

On the other hand, [MoSBi](https://exbio.wzw.tum.de/mosbi/) or Molecular Signatures with Biclustering is a software tool used to stratify samples based on lipidomics data (or any molecular omics data in general). The unique thing about this software is that it creates biclusters by combining several biclustering algorithms via an ensemble approach. This is to ensure that the bicluster results are more robust to changes in the data sets.

MoSBi is available as an [R package](https://github.com/tdrose/mosbi) in [Bioconductor](https://bioconductor.org/packages/release/bioc/html/mosbi.html), a [web service](https://exbio.wzw.tum.de/mosbi/) as well as the option to be created using [Docker](https://www.docker.com/) from this [GitLab website](https://gitlab.lrz.de/lipitum-projects/mosbi-webapp).

## Windows 10 set up

The minimal settings to have Docker with WSL 2 backend in Windows can be found in this installation web site (https://docs.docker.com/desktop/windows/install/)

![windows_requirements](images/windows_requirements.png)

The biggest challenge is to get WSL 2 to work in Windows 10.

While the list of requirements can be daunting, the good news is that the Docker Installer for Windows will help automatically download and install WSL 2 and will prompt you to update the WSL 2 Linux kernel as well after installation.

### Windows 10 specifications

A 64-bit processor with Second Level Address Translation (SLAT) and a minimum of 4GB system RAM are required to run WSL 2 on Windows 10.

Here are my Windows 10 settings

![windows_specification](images/windows_specification.png)

![windows_specification2](images/windows_specification2.png)

Clearly, the RAM part is satisfied and I am using a 64 bit machine.

To check if I have SLAT, firstly, ensure that you have administrative rights on your computer.

Go to Control Panel.

![control_panel](images/control_panel.png)

Click on Program in green.

![programs](images/programs.png)

Click on Turn Windows feature on or off.

![windows_features](images/windows_features.png)

Windows Feature will be opened and scroll down and expand Hyper-V and see if Hyper-V-Platform is not masked or grey out. If so, the CPU supports SLAT. This is because SLAT is required for a successful Hyper-V installation.

![slat_enabled](images/slat_enabled.png)

More information can be found in this [webpage](https://www.kunal-chowdhury.com/2012/11/second-level-address-translation-slat-in-hyperv.html)

### Enable Virtual Machine Platform Windows Feature

This is required for WSL 2 to work on Windows 10.

To enable this, firstly, ensure that you have administrative rights on your computer and internet connection.

Open Windows Feature (following the steps from the previous section Windows 10 specifications) and check on the box “Virtual Machine Platform” and click OK.

![virtual_machine_platform](images/virtual_machine_platform.png)

Windows will search the internet for the necessary files and apply the changes. You will be prompted to restart the computer after the change is applied.

### Virtualization enabled in the BIOS

This is required for WSL 2 to work on Windows 10.

I am using a Dell Optiplex 7071 Tower Desktop. According to this [specifications website](https://www.dell.com/support/manuals/en-sg/optiplex-7071-desktop/optiplex7071_setup/virtualization-support?guid=guid-e0672e00-c1cf-4ad5-9575-a1f762bae383&lang=en-us), the virtualization is enabled by default.

To confirm this, referring to this [stack overflow question](https://stackoverflow.com/questions/49005791/how-to-check-if-intel-virtualization-is-enabled-without-going-to-bios-in-windows#:~:text=If%20you%20have%20Windows%2010,is%20currently%20enabled%20in%20BIOS.), open Task Manager and click on the Performance Tab and then CPU.

Here my Virtualization settings is labelled as “Enabled”.

![visualization_task_manager](images/visualization_task_manager.png)

If it shows “Disabled”, you will need to enable it in BIOS. If you don’t see “Virtualization”, it means that the CPU does not support virtualization and Docker unfortunately cannot be used in this computer.

To enabled virtualization in BIOS from a Dell Optiplex 7071 Tower Desktop, you will need to get to the BIOS menu. To do so, restart the computer. When the monitor screen shows that the computer has switched off, press the “F12” button to access the Boot Options. Go to BIOS Setup and press Enter.

![boot_option](images/boot_option.png)

You will be led to this BIOS menu.

![boot_option](images/bios_menu.png)

Expand the Virtulization tab and click on Virtualization and check “Enable Intel Virtualization Technology”

![bios_menu_virtual_enabled](images/bios_menu_virtual_enabled.png)

Some computers may require this as well, click on VT for Direct I/O and check “Enable VT for Direct I/O”

![bios_menu_virtual_IO](images/bios_menu_virtual_IO.png)

## Docker in Windows 10

### Docker Desktop for Windows Installation

With the above Windows 10 settings completed, we can now proceed with the Docker installation.

Go to the Docker [installation website](https://docs.docker.com/desktop/windows/install/) to download Docker Desktop for Windows. The current Docker Desktop version is 4.8.2

![docker_windows_installer](images/docker_windows_installer.png)

Double click on this file will give the following. Check both boxes and click Ok.

![docker_windows_configuration](images/docker_windows_configuration.png)

Installation will proceed

![docker_windows_installation_process](images/docker_windows_installation_process.png)

and when it is done. Click Close and restart to allow Windows to restart and complete the installation.

![docker_windows_installation_done](images/docker_windows_installation_done.png)

After restarting, the Docker Desktop shortcut icon will appear.

![docker_desktop_icon](images/docker_desktop_icon.png)

Double click on this will lead to a service agreement. Check on “I accept the terms” anf click the Accept button.

![docker_service_agreement.png](images/docker_service_agreement.png)

### Installation of WSL 2 kernel update

After accepting the service agreement, a pop up will appear saying that WSL2 installtion is incomplete. This is because, we have yet to install the WSL 2 kernel updates.

![docker_wsl2_incomplete.png](images/docker_wsl2_incomplete.png)

No need to worry. Just click on the link provided and you should be let to this [webpage](https://docs.microsoft.com/en-us/windows/wsl/install). Do not attempt to close this message box as we will come back to it later.

![wsl2_kernel_webpage.png](images/wsl2_kernel_webpage.png)

Simply click “WSL 2 Linux kernel update package for x64 machines”

![wsl2_kernel_link.png](images/wsl2_kernel_link.png)

and double click on the installation file to give the Windows Subsystem for Linux Update setup wizard.

![wsl2_kernel_installation.png](images/wsl2_kernel_installation.png)
![wsl2_kernel_setup.png](images/wsl2_kernel_setup.png)

Click on Next to proceed with the installation.

![wsl2_kernel_installation_start](images/wsl2_kernel_installation_start.png)

Click on Finish to complete the installation.

![wsl2_kernel_installation_done](images/wsl2_kernel_installation_done.png)

Go back to this pop up message box and click Restart

![wsl2_kernel_restart](images/wsl2_kernel_restart.png)

This will allow Docker Desktop for Windows to restart

![docker_windows_restart](images/docker_windows_restart.png)

This time it should open without errors with this tutorial page.

![docker_windows_tutorial](images/docker_windows_tutorial.png)

You may wish to take time to go through the tutorial. Else you may skip it which will bring you to this home page.

![docker_homepage](images/docker_homepage.png)

To confirm that WSL 2 is successfully installed and it being used by Docker, go to Settings,

![docker_settings](images/docker_settings.png)

Look at the General Tab. You will see that “Use the WSL 2 based engine” should be checked.

![docker_general](images/docker_general.png)

With Docker installed in Windows 10, we can now proceed to run the two lipidomics software in the Docker environment.

## LINEX in Windows 10 Docker

The instruction to run LINEX using Docker can be found in this [GitLab webpage](https://gitlab.lrz.de/lipitum-projects/linex).

Nevertheless, I will try to provide a more detailed procedure on how this can be done in Windows 10 for the sake of those who are unfamiliar with the workings of Windows 10.

### Software download

The first step is to download the repository. For Windows 10, we can download it as a zip file.

![LINEX_download](images/LINEX_download.png)

To unzip it, right click the zip folder and click on Extract All…

![LINEX_unzip](images/LINEX_unzip.png)

In my example, I choose to extract it on the D drive.

![LINEX_destination](images/LINEX_destination.png)

![LINEX_in_D\_drive](images/LINEX_in_D_drive.png)

### Docker Excecution

After extraction, open Command Prompt in the current folder by going to the folder location and type “cmd” on the address bar.

![get_to_cmd](images/get_to_cmd.gif)

In this command prompt, type `docker-compose up -d` as instructed by the [GitLab webpage](https://gitlab.lrz.de/lipitum-projects/linex). This is what you should see.

![LINEX_success_run](images/LINEX_success_run.gif)

Once the process is completed, go back to Docker Desktop for Windows and click on Containers, Volumes and Images. This is what you should see.

![LINEX_container](images/LINEX_container.png)

![LINEX_volume](images/LINEX_volume.png)

![LINEX_image](images/LINEX_image.png)

### Running LINEX

With a working Docker container, we can open the LINEX web page in our local server using `http://127.0.0.1:8084` as recommended in the [GitLab website](https://gitlab.lrz.de/lipitum-projects/linex)

![LINEX_working_website](images/LINEX_working_website.gif)

### Closing session

We can close the container using the `docker-compose down`

![LINEX_end_container](images/LINEX_end_container.gif)

## MoSBi in Windows 10 Docker

The instruction to run MoSBi web application using Docker can be found in this [GitLab webpage](https://gitlab.lrz.de/lipitum-projects/mosbi-webapp).

The steps are similar to the previous section.

### Software download

Download the repository first. For Windows 10, we can download it as a zip file.

![MoSBi_download](images/MoSBi_download.png)

To unzip it, right click the zip folder and click on Extract All…

![MoSBi_unzip](images/MoSBi_unzip.png)

In my example, I choose to extract it on the D drive.

![MoSBi_destination](images/MoSBi_destination.png)

![MoSBi_in_D\_drive](images/MoSBi_in_D_drive.png)

### Docker Excecution

After extraction, open Command Prompt in the current folder by going to the folder location and type “cmd” on the address bar.

![MoSBi_get_to_cmd](images/MoSBi_get_to_cmd.gif)

In this command prompt, type `docker-compose up` as instructed by the [GitLab webpage](https://gitlab.lrz.de/lipitum-projects/mosbi-webapp). The process will take some time to run but this is what you should see when everything is done.

In this scenario, **do not** close the command prompt.

![MoSBi_working_shiny](images/MoSBi_working_shiny.gif)

In the Docker Desktop for Windows, the following Containers and Images will be running

![MoSBi_container](images/MoSBi_container.png)

![MoSBi_image](images/MoSBi_image.png)

### Running MoSBi

With a working Docker container, we can open the MoSBi web page in our local server using `http://127.0.0.1:8082` as recommended in the [GitLab website](https://gitlab.lrz.de/lipitum-projects/mosbi-webapp)

![MoSBi_working_website](images/MoSBi_working_website.gif)

When the web page is running, a new container will be created in Docker Desktop for Windows. In my example, it is called “optimistic_shtern”.

![MoSBi_shiny_container](images/MoSBi_shiny_container.png)

### Closing session

To stop the web service, go back to the command prompt and press “Ctrl+C” on the keyboard. This is what you should see.

![MoSBi_end_container](images/MoSBi_end_container.gif)

After that, remember to go back to Docker Desktop for Windows and stop the `mobishiny` container from running.

![MoSBi_end_shiny_container](images/MoSBi_end_shiny_container.png)

## Conclusion

If you have followed me this far successfully 😅, then congratulations 🎉, you have managed to recreate two open source web applications 🌐 using Docker 🐳. Unfortunately, I have to apologise 😓 that I lack the knowledge currently to fully explain why these Docker command works and what is it doing. For now, I am just going to try out these cool web applications.

Once again, I do hope this is helpful in your learning journey with Docker 🐳 and to see its usefulness in recreating someone else’s open source software.

## References

<div id="refs" class="references csl-bib-body">

<div id="ref-LINEX2021" class="csl-entry">

<span class="csl-left-margin">1. </span><span class="csl-right-inline">Köhler N, Rose TD, Falk L, Pauling JK. Investigating global lipidome alterations with the lipid network explorer. Metabolites \[Internet\]. 2021;11(8). Available from: <https://www.mdpi.com/2218-1989/11/8/488></span>

</div>

<div id="ref-LINEX2022" class="csl-entry">

<span class="csl-left-margin">2. </span><span class="csl-right-inline">Rose TD, Köhler N, Falk L, Klischat L, Lazareva OE, Pauling JK. Lipid network and moiety analysis for revealing enzymatic dysregulation and mechanistic alterations from lipidomics data. bioRxiv \[Internet\]. 2022; Available from: <https://www.biorxiv.org/content/early/2022/05/23/2022.02.04.479101></span>

</div>

<div id="ref-MoSBi" class="csl-entry">

<span class="csl-left-margin">3. </span><span class="csl-right-inline">Rose TD, Bechtler T, Ciora OA, Le KAL, Molnar F, Köhler N, et al. MoSBi: Automated signature mining for molecular stratification and subtyping. Proceedings of the National Academy of Sciences \[Internet\]. 2022;119(16):e2118210119. Available from: <https://www.pnas.org/doi/abs/10.1073/pnas.2118210119></span>

</div>

</div>