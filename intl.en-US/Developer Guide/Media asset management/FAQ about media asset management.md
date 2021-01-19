FAQ about media asset management 
=====================================================



How do I delete a stream in a specific definition? 
-----------------------------------------------------------------------

Call the [GetPlayInfo](/intl.en-US/API Reference/Video playback/GetPlayInfo.md) operation to obtain the ID of the stream that you want to delete. The ID of the stream is specified by the JobId parameter. Then, call the [DeleteStream](/intl.en-US/API Reference/Media management/Audio&Video Management/DeleteStream.md) operation to delete the stream.

How do I delete the old stream after retranscoding? 
------------------------------------------------------------------------

To ensure smooth switching from old streams to new streams, the system keeps old stream files after retranscoding. By default, the GetPlayInfo operation returns the latest transcoded stream in each definition and format to ensure that the latest transcoded stream is played each time. When you call the [GetPlayInfo](/intl.en-US/API Reference/Video playback/GetPlayInfo.md) operation, you can set `ResultType` to **Multiple** to obtain all transcoded streams for the audio or video. You can obtain the IDs of old streams based on the creation time of the streams and then delete the old streams.

How do I delete an encrypted stream? 
---------------------------------------------------------

By default, playback operations return only unencrypted streams. This ensures the security of stream information. When you call the [GetPlayInfo](/intl.en-US/API Reference/Video playback/GetPlayInfo.md) operation, you can set `ResultType` to **Multiple** to obtain all transcoded streams for the audio or video. You can obtain the IDs of encrypted streams based on the `Encrypt` parameter in the [PlayInfo](/intl.en-US/API Reference/Appendix/Basic data types.md) structure and then delete the encrypted streams.
