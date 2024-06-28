.. _api_shader_stage_control:

API Shader Stage Control
========================

Several views in RGP provide information about which API shader stages are active
for a particular event or pipeline. This information is represented by the API Shader
Stage control.

**NOTE**: This control is only available for DirectX and Vulkan profiles.

This control appears in the **Most expensive events** and **Pipelines** Overview panes, as well
as in the Details side panel in the **Wavefront occupancy** and **Event timings** panes, and in the
toolbar area of the **Instruction timing** pane.

Here are examples of what the control looks like for a few different DirectX12 and Vulkan pipelines.

DirectX12 pipeline with the VS and PS stages active:

.. image:: media_rgp/rgp_dx12_pipeline_stage_vs_ps.png

DirectX12 pipeline with the VS, HS, DS and PS stages active:

.. image:: media_rgp/rgp_dx12_pipeline_stage_vs_hs_ds_ps.png

DirectX12 pipeline with the VS, GS and PS stages active:

.. image:: media_rgp/rgp_dx12_pipeline_stage_vs_gs_ps.png

DirectX12 pipeline with the CS stages active:

.. image:: media_rgp/rgp_dx12_pipeline_stage_cs.png

DirectX12 pipeline with the RT stages active:

.. image:: media_rgp/rgp_dx12_pipeline_stage_rt.png

Vulkan pipeline with the VS and FS stages active:

.. image:: media_rgp/rgp_vk_pipeline_stage_vs_fs.png

Vulkan pipeline with the CS stages active:

.. image:: media_rgp/rgp_vk_pipeline_stage_cs.png

Vulkan pipeline with the RT stages active:

.. image:: media_rgp/rgp_vk_pipeline_stage_rt.png

This control can also indicate when a particular shader stage contains inline ray
tracing. When this is detected, a stage will indicate this with a gradient red
pattern painted in that stage's box. Here is an example of a DirectX12 pipeline
where the compute shader performs inline ray tracing:

.. image:: media_rgp/rgp_dx12_pipeline_stage_cs_with_inline_rt.png