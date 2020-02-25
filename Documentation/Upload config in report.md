## Upload config in report

Take config from when we import the metadata and use that when we generate the report.

03/10/2019

- added it into node_config_functions in dce_reports/sections
- added method add_config to upload_msg class in dce_datagraph/api_messages
- added self.config = [] and upload param also
- added add_upload_node_config function to dce_reports/datamap_report/widget_config