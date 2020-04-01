---
layout: single
classes: wide
title: Installing CUDA 7.5 in Ubuntu 14.04
date: 2016-03-22
tags: [cuda, ubuntu]
category: blog
---

After some problems installing CUDA 7.5 in Ubuntu 14.04, facing login loops and other problems, I found a solution on a NVIDIA forum (link in the end of the post). This procedure installs the graphics card for CUDA purposes, not allowing its use for rendering.

1. Install the build-essentials package by running:   
{% highlight sh %}
  sudo apt-get install build-essential
{% endhighlight %}

2. Download the CUDA installation (.run) file from the NVIDIA website ([Link](https://developer.nvidia.com/cuda-downloads)).

3. If you have a xorg.conf file, remove it (backup the file first to avoid any problems):    
{% highlight sh %}
  sudo mv /etc/X11/xorg.conf.bkp
{% endhighlight %}

4. Create the /etc/modprobe.d/blacklist-nouveau.conf file containing:   
    <pre>
      blacklist nouveau
      option nouveau modeset=0
    </pre>

5. The run the following command and reboot your computer.   
{% highlight sh %}
  sudo update-initramfs -u
{% endhighlight %}

6. When the login screen appears, type Ctrl + Alt + F1 to access the text interface and login with your user.

7. Go to the directory where the CUDA .run file was downloaded and run:   
{% highlight sh %}
  chmod a+x CUDA_RUN_FILE
{% endhighlight %}

8. Stop the lightdm service and run the CUDA installation file (__OpenGL libs should not be installed!__):   
{% highlight sh %}
  sudo service lightdm stop    
  sudo bash cuda-7.0.28_linux.run --no-opengl-libs
{% endhighlight %}

9. During the installation you should __ACCEPT__ the EULA conditions, say __YES__ to installing the NVIDIA driver, __YES__ to installing the CUDA Toolkit and Driver and __YES__ to installing the CUDA Samples. If asked, you should say __NO__ when asked if you want to rebuild any Xserver configurations.

10. After the installation is complete, check if device nodes are present (if nothing happens, it means everything is ok!):   
{% highlight sh %}
  sudo modprobe nvidia
{% endhighlight %}

11. Set environment path variables (this can be added to the end of the XXXXXX file so that there is no need to rerun this commands every time you restart your computer). Remember to change YOUR_CUDA_PATH to the right path, depending on your CUDA version (e.g. /usr/local/cuda-7.5):   
{% highlight sh %}
  export PATH=YOUR_CUDA_PATH/bin:$PATH     
  export LD_LIBRARY_PATH=YOUR_CUDA_PATH/lib64:$LD_LIBRARY_PATH
{% endhighlight %}

12. Verify the NVIDIA driver version and the CUDA driver version:   
{% highlight sh %}
  cat /proc/driver/nvidia/version    
  nvcc -V
{% endhighlight %}

13. (Optional) Now, you can switch the lightdm back on. You should then be able to login through the GUI without any problems:   
{% highlight sh %}
  sudo service lightdm start
{% endhighlight %}

__To test the CUDA installation:__

14. Create the CUDA Samples by accessing its folder and running:
{% highlight sh %}
  make
{% endhighlight %}

15. Go to the release folder inside the CUDA Samples folder (e.g. NVIDIA_CUDA-7.5_Samples/bin/x86_64/linux/release/) and run two standard checks (first to see your graphics card specs and then to check if its operating correctly). Both tests should ouput 'PASS':   
{% highlight sh %}
  ./deviceQuery     
  ./bandwidthTest
{% endhighlight %}

Everything should be ok after you reboot.   


_Source: [Titan X for CUDA 7.5 login-loop error](https://devtalk.nvidia.com/default/topic/878117/-solved-titan-x-for-cuda-7-5-login-loop-error-ubuntu-14-04-/)_
