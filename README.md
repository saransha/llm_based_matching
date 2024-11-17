# llm_based_matching

Reconciling Lists

1. Fuzzy Matching for Preliminary Candidates to generate short context
Use a fuzzy matching algorithm (e.g., Levenshtein distance or cosine similarity) to create a list of potential matches:
For each item in List 2, find the top 3 closest matches from List 1.
Return the top 3 possible matches. 
2.  LLM Matching Refinement
Input Selection: Pass only the top 3 fuzzy matches from list 1 for each item in list 2 to an LLM for further analysis.
LLM Matching: Use the LLM to assess the quality of matches:
The LLM will determine whether each candidate is an Exact Match, or Different Values, or No Match based on VIN similarities and associated attributes and also generate the details columns. 
3. Handle Unmatched Items from List and Generate Comprehensive Output
Rename No Match to List 2 only
Determine items only in List 1 using the output of the LLMs and append rows to generate final output
 
Tradeoffs - 

LLMs increase cost of computation when compared to only using a fuzzy matching algorithm but are highly accurate, and tailored to handle the ambiguous use case of Vin formatting difference and differences in years. Missing a match will be very costly to the brokerage so the aim is to build a precise system that can best handle these ambiguities justifying the increase in computation cost. It also allows us to easily generate the Details column with similarities and differences which will be very useful to the brokerage. By preprocessing the data with fuzzy matching we allow for minimal calls to LLM as we can manually add the remaining rows from list 1 without any calls to the LLMs
