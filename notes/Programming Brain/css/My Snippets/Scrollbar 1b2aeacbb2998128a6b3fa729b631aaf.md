# Scrollbar

A scrollbar is an interaction technique or widget in which continuous text, pictures, or any other content can be scrolled in a predetermined direction (up, down, left, or right) on a computer display, window, or viewport so that all of the content can be viewed

---

- Hidden Scrollbar Entire Website
    
    Scrollbars consist of various elements that can be styled individually, using specific CSS pseudo-elements for WebKit-based browsers (like Chrome, Safari, and Opera) and Firefox. The key pseudo-elements for customizing scrollbars include:
    
    - ::-webkit-scrollbar: The entire scrollbar.
    - ::-webkit-scrollbar-track: The track (background) of the scrollbar.
    - ::-webkit-scrollbar-thumb: The draggable part of the scrollbar.
    - ::-webkit-scrollbar-button: Optional buttons on the scrollbar (not commonly used).
    - ::-moz-scrollbar, ::-moz-scrollbar-track, ::-moz-scrollbar-thumb: For customizing Firefox scrollbars.
    
    ```css
    ::-webkit-scrollbar {
      display: none;
    }
    
    * {
      scrollbar-width: none; /* Firefox */
      -ms-overflow-style: none;  /* Internet Explorer 10+ */
    }
    ```
    
- Hidden Scrollbar For Specific Element
    
    Scrollbars consist of various elements that can be styled individually, using specific CSS pseudo-elements for WebKit-based browsers (like Chrome, Safari, and Opera) and Firefox. The key pseudo-elements for customizing scrollbars include:
    
    - ::-webkit-scrollbar: The entire scrollbar.
    - ::-webkit-scrollbar-track: The track (background) of the scrollbar.
    - ::-webkit-scrollbar-thumb: The draggable part of the scrollbar.
    - ::-webkit-scrollbar-button: Optional buttons on the scrollbar (not commonly used).
    - ::-moz-scrollbar, ::-moz-scrollbar-track, ::-moz-scrollbar-thumb: For customizing Firefox scrollbars.
    
    ```css
    .scroll-container {
      height: 150px;
      overflow: scroll;
      -ms-overflow-style: none; /* Internet Explorer, Edge */
    
      scrollbar-width: none; /* Firefox */
    }
    
    .scroll-container::-webkit-scrollbar {
      display: none; /* Chrome, Safari, and Opera */
    }
    ```
    
- Customize Scrollbar For Entire Website
    
    Scrollbars consist of various elements that can be styled individually, using specific CSS pseudo-elements for WebKit-based browsers (like Chrome, Safari, and Opera) and Firefox. The key pseudo-elements for customizing scrollbars include:
    
    - ::-webkit-scrollbar: The entire scrollbar.
    - ::-webkit-scrollbar-track: The track (background) of the scrollbar.
    - ::-webkit-scrollbar-thumb: The draggable part of the scrollbar.
    - ::-webkit-scrollbar-button: Optional buttons on the scrollbar (not commonly used).
    - ::-moz-scrollbar, ::-moz-scrollbar-track, ::-moz-scrollbar-thumb: For customizing Firefox scrollbars.
    
    ```css
    ::-webkit-scrollbar {
      width: 12px;
    }
    
    ::-webkit-scrollbar-track {
      background: #f1f1f1;
    }
    
    ::-webkit-scrollbar-thumb {
      background: #888;
    }
    
    ::-webkit-scrollbar-thumb:hover {
      background: #555;
    }
    
    ::-webkit-scrollbar-button {
      display: none;
    }
    ```
    
- Customize Scrollbar For Specific Element
    
    Scrollbars consist of various elements that can be styled individually, using specific CSS pseudo-elements for WebKit-based browsers (like Chrome, Safari, and Opera) and Firefox. The key pseudo-elements for customizing scrollbars include:
    
    - ::-webkit-scrollbar: The entire scrollbar.
    - ::-webkit-scrollbar-track: The track (background) of the scrollbar.
    - ::-webkit-scrollbar-thumb: The draggable part of the scrollbar.
    - ::-webkit-scrollbar-button: Optional buttons on the scrollbar (not commonly used).
    - ::-moz-scrollbar, ::-moz-scrollbar-track, ::-moz-scrollbar-thumb: For customizing Firefox scrollbars.
    
    ```css
    .scroll-container {
      height: 300px;
      overflow-y: scroll;
    }
    
    .scroll-container::-webkit-scrollbar {
      width: 12px;
    }
    
    .scroll-container::-webkit-scrollbar-track {
      background: #f1f1f1;
    }
    
    .scroll-container::-webkit-scrollbar-thumb {
      background: #888;
    }
    
    .scroll-container::-webkit-scrollbar-thumb:hover {
      background: #555;
    }
    
    .scroll-container::-webkit-scrollbar-button {
      display: none;
    }
    ```
    
- Scrollbar Always Stay on Botom
    
    This will scroll the message container to the bottom. Since scroll position is recorded in pixel and not percentage, the scroll position doesn't change as you add more elements into the container by default.
    
    ```jsx
    var objDiv = document.getElementById("parentDiv");
    objDiv.scrollTop = objDiv.scrollHeight;
    ```