# DataSave
@RequestMapping(value = "/test", method = RequestMethod.POST)
	public String getValuefromimag(final ModelMap model){
		Thread recordThread = new Thread() {
			@Override
			public void run() {
				int cnt = 0;
				try {
					int count=1;
					while (cnt == 0 || record) {
						ITesseract image = new Tesseract();   
						image.setDatapath("C:/Users/hp/Documents/NetBeansProjects/DisplayVolume/dist/lib");
						String str= image.doOCR(new File(store+"/"+count+".jpeg"));
						MyDatas data =dSave(str);
						model.addAttribute("sendData",data.getFirst());
						if (cnt == 0) {
							record = true;
							cnt = 1;
						}
						count=count+1;
					}

				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		};
		recordThread.start();
		return "start";
	}
