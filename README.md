### INSTALLATION:

1. Go to your AOSP directory:
**cd \<your-aosp-directory>**
2. Clone git repository:
**git clone https://github.com/xaidarrr/globallayer.git**
3. Add directory to your build
For example add this to the end of **device/google/cuttlefish/shared/auto/device_vendor.mk** if you want build car image:
>PRODUCT_SOONG_NAMESPACE += globallayer
PRODUCT_PACKAGES += \\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ntop \\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;libncurses

4. Configure sepolicy:
- Add this at the end of file_contexts:
> /vendor/bin/ntop u:object_r:ntop_exec:s0
- Create ntop.te file and add this there:
>type ntop, domain;
type ntop_exec, exec_type, vendor_file_type, file_type;
>
>domain_auto_trans(shell, ntop_exec, ntop)
>
>permissive ntop;

If you followed file path from previous point then file_contexts & ntop.te should be located here: **device/google/cuttlefish/shared/sepolicy/vendor/**

### BUILD:
If you followed file path which were written in Installation then to build this you should do this:
>source build/envsetup.sh
>lunch aosp_cf_x86_64_auto-trunk_staging-userdebug
>m
