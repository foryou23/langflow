---
title: Processing
slug: /components-processing
---

# Processing components in Langflow

Processing components process and transform data within a flow.

## Use a processing component in a flow

The **Split Text** processing component in this flow splits the incoming [Data](/concepts-objects) into chunks to be embedded into the vector store component.

The component offers control over chunk size, overlap, and separator, which affect context and granularity in vector store retrieval results.

![](/img/vector-store-document-ingestion.png)

## Alter Metadata

This component modifies metadata of input objects. It can add new metadata, update existing metadata, and remove specified metadata fields. The component works with both [Message](/concepts-objects) and [Data](/concepts-objects) objects, and can also create a new Data object from user-provided text.

### Inputs

| Name | Display Name | Info |
|------|--------------|------|
| input_value | Input | Objects to which Metadata should be added |
| text_in | User Text | Text input; value will be in 'text' attribute of Data object. Empty text entries are ignored. |
| metadata | Metadata | Metadata to add to each object |
| remove_fields | Fields to Remove | Metadata Fields to Remove |

### Outputs

| Name | Display Name | Info |
|------|--------------|------|
| data | Data | List of Input objects, each with added Metadata |

## Combine Text

This component concatenates two text sources into a single text chunk using a specified delimiter.

### Inputs

| Name | Display Name | Info |
|------|--------------|------|
| first_text | First Text | The first text input to concatenate. |
| second_text | Second Text | The second text input to concatenate. |
| delimiter | Delimiter | A string used to separate the two text inputs. Defaults to a space. |


## DataFrame operations

This component performs the following operations on Pandas [DataFrame](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html):

| Operation | Description | Required Inputs |
|-----------|-------------|-----------------|
| Add Column | Adds a new column with a constant value | new_column_name, new_column_value |
| Drop Column | Removes a specified column | column_name |
| Filter | Filters rows based on column value | column_name, filter_value |
| Head | Returns first n rows | num_rows |
| Rename Column | Renames an existing column | column_name, new_column_name |
| Replace Value | Replaces values in a column | column_name, replace_value, replacement_value |
| Select Columns | Selects specific columns | columns_to_select |
| Sort | Sorts DataFrame by column | column_name, ascending |
| Tail | Returns last n rows | num_rows |

### Inputs

| Name | Display Name | Info |
|------|--------------|------|
| df | DataFrame | The input DataFrame to operate on. |
| operation | Operation | Select the DataFrame operation to perform. Options: Add Column, Drop Column, Filter, Head, Rename Column, Replace Value, Select Columns, Sort, Tail |
| column_name | Column Name | The column name to use for the operation. |
| filter_value | Filter Value | The value to filter rows by. |
| ascending | Sort Ascending | Whether to sort in ascending order. |
| new_column_name | New Column Name | The new column name when renaming or adding a column. |
| new_column_value | New Column Value | The value to populate the new column with. |
| columns_to_select | Columns to Select | List of column names to select. |
| num_rows | Number of Rows | Number of rows to return (for head/tail). Default: 5 |
| replace_value | Value to Replace | The value to replace in the column. |
| replacement_value | Replacement Value | The value to replace with. |

### Outputs

| Name | Display Name | Info |
|------|--------------|------|
| output | DataFrame | The resulting DataFrame after the operation. |

## Filter Data

This component filters a Data object based on a list of keys.

### Inputs

| Name | Display Name | Info |
|------|--------------|------|
| data | Data | Data object to filter. |
| filter_criteria | Filter Criteria | List of keys to filter by. |

### Outputs

| Name | Display Name | Info |
|------|--------------|------|
| filtered_data | Filtered Data | A new Data object containing only the key-value pairs that match the filter criteria. |


## Parse JSON

This component converts and extracts JSON fields using JQ queries.

### Inputs

| Name | Display Name | Info |
|------|--------------|------|
| input_value | Input | Data object to filter. Can be a message or data object. |
| query | JQ Query | JQ Query to filter the data. The input is always a JSON list. |

### Outputs

| Name | Display Name | Info |
|------|--------------|------|
| filtered_data | Filtered Data | Filtered data as a list of data objects. |

## Merge Data component

This component combines multiple data sources into a single unified Data object.

The component iterates through the input list of data objects, merging them into a single data object. If the input list is empty, it returns an empty data object. If there's only one input data object, it returns that object unchanged. The merging process uses the addition operator to combine data objects.

### Inputs

| Name | Display Name | Info |
|------|--------------|------|
| data | Data | A list of data objects to be merged |

### Outputs

| Name | Display Name | Info |
|------|--------------|------|
| merged_data | Merged Data | A single data object containing the combined information from all input data objects |


## Parse Data

The ParseData component converts data objects into plain text using a specified template.
This component transforms structured data into human-readable text formats, allowing for customizable output through the use of templates.

### Inputs

| Name | Display Name | Info |
|------|--------------|------|
| data | Data | The data to convert to text. |
| template | Template | The template to use for formatting the data. It can contain the keys `{text}`, `{data}` or any other key in the data. |
| sep | Separator | The separator to use between multiple data items. |

### Outputs

| Name | Display Name | Info |
|------|--------------|------|
| text | Text | The resulting formatted text string as a message object. |


## Split Text

This component splits text into chunks of a specified length.

### Inputs

| Name | Display Name | Info |
|------|--------------|------|
| texts | Texts | Texts to split. |
| separators | Separators | Characters to split on. Defaults to a space. |
| max_chunk_size | Max Chunk Size | The maximum length, in characters, of each chunk. |
| chunk_overlap | Chunk Overlap | The amount of character overlap between chunks. |
| recursive | Recursive | Whether to split recursively. |

## LLM Router

This component routes requests to the most appropriate LLM based on OpenRouter model specifications.

### Inputs

| Name | Display Name | Info |
|------|--------------|------|
| models | Language Models | List of LLMs to route between |
| input_value | Input | The input message to be routed |
| judge_llm | Judge LLM | LLM that will evaluate and select the most appropriate model |
| optimization | Optimization | Optimization preference (quality/speed/cost/balanced) |

### Outputs

| Name | Display Name | Info |
|------|--------------|------|
| output | Output | The response from the selected model |
| selected_model | Selected Model | Name of the chosen model |

## Merge Data (Data Combiner)

This component combines data using different operations.

### Inputs

| Name | Display Name | Info |
|------|--------------|------|
| data_inputs | Data Inputs | Data to combine (minimum 2 inputs required) |
| operation | Operation Type | Operation to perform (Concatenate/Append/Merge/Join) |

### Outputs

| Name | Display Name | Info |
|------|--------------|------|
| combined_data | DataFrame | The combined data result |

## Message to Data

This component converts Message objects to Data objects.

### Inputs

| Name | Display Name | Info |
|------|--------------|------|
| message | Message | The Message object to convert to a Data object |

### Outputs

| Name | Display Name | Info |
|------|--------------|------|
| data | Data | The converted Data object |

## Parse Data (Data to Message)

This component converts Data objects into Messages using templated formatting.

### Inputs

| Name | Display Name | Info |
|------|--------------|------|
| data | Data | The data to convert to text (can be list) |
| template | Template | Template for formatting (`{text}`, `{data`, or any key in Data) |
| sep | Separator | Separator between multiple data items |

### Outputs

| Name | Display Name | Info |
|------|--------------|------|
| text | Message | Data as a single Message |
| data_list | Data List | Data as list of new Data objects |

## Parse DataFrame

This component converts DataFrames into plain text using templates.

### Inputs

| Name | Display Name | Info |
|------|--------------|------|
| df | DataFrame | The DataFrame to convert to text rows |
| template | Template | Template for formatting (use `{column_name}` placeholders) |
| sep | Separator | String to join rows in output |

### Outputs

| Name | Display Name | Info |
|------|--------------|------|
| text | Text | All rows combined into single text |

## Parse JSON Data

This component converts and extracts JSON fields using JQ queries.

### Inputs

| Name | Display Name | Info |
|------|--------------|------|
| input_value | Input | Data object to filter (Message or Data) |
| query | JQ Query | JQ Query to filter the data |

### Outputs

| Name | Display Name | Info |
|------|--------------|------|
| filtered_data | Filtered Data | Filtered data as list of Data objects |

## Select Data

This component selects a single data item from a list.

### Inputs

| Name | Display Name | Info |
|------|--------------|------|
| data_list | Data List | List of data to select from |
| data_index | Data Index | Index of the data to select |

### Outputs

| Name | Display Name | Info |
|------|--------------|------|
| selected_data | Selected Data | The selected Data object |

## Split Text

This component splits text into chunks based on specified criteria.

### Inputs

| Name | Display Name | Info |
|------|--------------|------|
| data_inputs | Data Inputs | The data to split |
| chunk_overlap | Chunk Overlap | Number of characters to overlap between chunks |
| chunk_size | Chunk Size | Maximum number of characters in each chunk |
| separator | Separator | Character to split on (defaults to newline) |

### Outputs

| Name | Display Name | Info |
|------|--------------|------|
| chunks | Chunks | List of split text chunks as Data objects |
| dataframe | DataFrame | The chunks as a DataFrame |

## Update Data

This component dynamically updates or appends data with specified fields.

### Inputs

| Name | Display Name | Info |
|------|--------------|------|
| old_data | Data | The records to update |
| number_of_fields | Number of Fields | Number of fields to add (max 15) |
| text_key | Text Key | Key for text content |
| text_key_validator | Text Key Validator | Validates text key presence |

### Outputs

| Name | Display Name | Info |
|------|--------------|------|
| data | Data | Updated Data objects |
