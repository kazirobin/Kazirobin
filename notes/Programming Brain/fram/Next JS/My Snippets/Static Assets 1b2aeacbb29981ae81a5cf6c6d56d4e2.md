# Static Assets

Access static files in the public folder at runtime but would prefer a simple solution that works with next you can do the following:

Create a file named `./src/app/api/public/[[…slug]].js`

```jsx
import fs from "fs";
import { NextRequest, NextResponse } from "next/server";
import path from "path";

export async function GET(req: NextRequest, content: any) {
  const slug = content.params.slug;

  if (slug && slug.length) {
    const publicDir = path.join(process.cwd(), "public");
    const fileUrl = slug.join("/");
    const filePath = path.join(publicDir, fileUrl);

    try {
      const data = await fs.promises.readFile(filePath);
      return new NextResponse(data, { status: 200 });
    } catch (error) {
      return new NextResponse(null, { status: 404 });
    }
  } else {
    return new NextResponse(null, { status: 400 });
  }
}
```

Now you can access the files in your public folder using `"yourapplication:3000/api/public/*”`

Example: `<img src="/api/public/uploads/images/myimage.jpg">`