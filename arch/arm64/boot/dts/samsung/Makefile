ifeq ($(CONFIG_BUILD_ARM64_DT_OVERLAY),y)

# GTS4LV EUR
SEC_GTS4LV_EUR_DTBO := \
		sdm670-sec-gts4lv-eur-overlay-r00.dtbo \
		sdm670-sec-gts4lv-eur-overlay-r01.dtbo \
		sdm670-sec-gts4lv-eur-overlay-r02.dtbo \
		sdm670-sec-gts4lv-eur-overlay-r03.dtbo \
		sdm670-sec-gts4lv-eur-overlay-r04.dtbo \
		sdm670-sec-gts4lv-eur-overlay-r05.dtbo
		
# GTS4LV WIFI
SEC_GTS4LVWIFI_EUR_DTBO := \
		sdm670-sec-gts4lvwifi-eur-overlay-r02.dtbo \
		sdm670-sec-gts4lvwifi-eur-overlay-r03.dtbo \
		sdm670-sec-gts4lvwifi-eur-overlay-r04.dtbo \
		sdm670-sec-gts4lvwifi-eur-overlay-r05.dtbo
		
# GTS4LV KOR
SEC_GTS4LV_KOR_DTBO := \
		sdm670-sec-gts4lv-kor-overlay-r02.dtbo \
		sdm670-sec-gts4lv-kor-overlay-r03.dtbo \
		sdm670-sec-gts4lv-kor-overlay-r04.dtbo \
		sdm670-sec-gts4lv-kor-overlay-r05.dtbo

# GTS4LV MEA
SEC_GTS4LV_MEA_DTBO := \
		sdm670-sec-gts4lv-mea-overlay-r01.dtbo \
		sdm670-sec-gts4lv-mea-overlay-r02.dtbo \
		sdm670-sec-gts4lv-mea-overlay-r03.dtbo \
		sdm670-sec-gts4lv-mea-overlay-r04.dtbo \
		sdm670-sec-gts4lv-mea-overlay-r05.dtbo

# GTS4LV USA
SEC_GTS4LV_USA_DTBO := \
		sdm670-sec-gts4lv-usa-overlay-r04.dtbo

define __sec_dtbo_build
dtbo-$(2) += $(1)
$(1)-base := $(3)
endef

define sec_dtbo_build
$(foreach dtbo, $(1), $(eval $(call __sec_dtbo_build, $(dtbo),$(2),$(3))))
endef

# SDM670 BASE DTB
SEC_SDM670_BASE_DTB := ../qcom/sdm670.dtb

$(eval $(call sec_dtbo_build, \
		$(SEC_GTS4LV_EUR_DTBO),$(CONFIG_SEC_GTS4LV_EUR_PROJECT),$(SEC_SDM670_BASE_DTB)))

$(eval $(call sec_dtbo_build, \
		$(SEC_GTS4LVWIFI_EUR_DTBO),$(CONFIG_SEC_GTS4LVWIFI_EUR_PROJECT),$(SEC_SDM670_BASE_DTB)))
		
$(eval $(call sec_dtbo_build, \
		$(SEC_GTS4LVWIFI_EUR_DTBO),$(CONFIG_SEC_GTS4LVWIFI_EUR_LDU_PROJECT),$(SEC_SDM670_BASE_DTB)))

$(eval $(call sec_dtbo_build, \
		$(SEC_GTS4LV_KOR_DTBO),$(CONFIG_SEC_GTS4LV_KOR_PROJECT),$(SEC_SDM670_BASE_DTB)))

$(eval $(call sec_dtbo_build, \
		$(SEC_GTS4LV_MEA_DTBO),$(CONFIG_SEC_GTS4LV_MEA_PROJECT),$(SEC_SDM670_BASE_DTB)))

$(eval $(call sec_dtbo_build, \
		$(SEC_GTS4LV_USA_DTBO),$(CONFIG_SEC_GTS4LV_USA_PROJECT),$(SEC_SDM670_BASE_DTB)))
else

ifeq ($(filter y,$(CONFIG_MACH_A8SQLTE_CHN_OPEN) $(CONFIG_MACH_A8SQLTE_CHN_LDU)),y)
dtb-y += \
	sdm710-sec-a8sqlte-chn-r00.dtb \
	sdm710-sec-a8sqlte-chn-r01.dtb \
	sdm710-sec-a8sqlte-chn-r02.dtb \
	sdm710-sec-a8sqlte-chn-r03.dtb \
	sdm710-sec-a8sqlte-chn-r04.dtb \
	sdm710-sec-a8sqlte-chn-r05.dtb
endif

dtb-$(CONFIG_MACH_A8SQLTE_CHN_TW) += \
				sdm710-sec-a8sqlte-chn_tw-r04.dtb

ifeq ($(filter y,$(CONFIG_MACH_A8SQLTE_KOR_SINGLE) $(CONFIG_MACH_A8SQLTE_KOR_LDU)),y)
dtb-y += \
	sdm710-sec-a8sqlte-kor-r02.dtb \
	sdm710-sec-a8sqlte-kor-r03.dtb \
	sdm710-sec-a8sqlte-kor-r04.dtb
endif
endif

ifeq ($(CONFIG_ARM64),y)
always          := $(dtb-y)
subdir-y        := $(dts-dirs)
else
targets += dtbs
targets += $(addprefix ../, $(dtb-y))

$(obj)/../%.dtb: $(src)/%.dts FORCE
        $(call if_changed_dep,dtc)

dtbs: $(addprefix $(obj)/../,$(dtb-y))
endif
clean-files := *.dtb *.reverse.dts *.dtbo

