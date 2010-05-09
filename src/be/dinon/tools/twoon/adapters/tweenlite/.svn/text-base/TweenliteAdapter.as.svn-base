package be.dinon.tools.twoon.adapters.tweenlite
{
	import be.dinon.tools.twoon.adapters.TwoonAdapter;
	import be.dinon.tools.twoon.adapters.TwoonAdapterAbstract;
	import be.dinon.tools.twoon.enums.TwoonEasingMovement;
	import be.dinon.tools.twoon.enums.TwoonEasingType;
	import be.dinon.tools.twoon.enums.TwoonFromToType;
	import be.dinon.tools.twoon.errors.TwoonError;
	import be.dinon.tools.twoon.vos.TwoonValue;
	
	import com.greensock.TweenLite;
	
	public class TweenliteAdapter extends TwoonAdapterAbstract implements TwoonAdapter
	{
		private var tween:TweenLite;
		
		public function TweenliteAdapter()
		{
			// this : for fake abstract impl
			super(this);
		}
		
		override public function start():void 
		{
			super.start();
			
			var fromValues:Array = getFromValues();
			var toValues:Array = getToValues();
			var props:Object;// = getVarsObject();
			if (fromValues.length > 0 && toValues.length > 0)
			{
				for each(var value:TwoonValue in fromValues)
				{
					target[value.property.name] = value.fromValue;
				}
				props = getVarsObject(TwoonFromToType.TO);
				tween = TweenLite.to(target, getDurationInSeconds(), props);
			}
			else if (fromValues.length > 0)
			{
				props = getVarsObject(TwoonFromToType.FROM);
				tween = TweenLite.from(target, getDurationInSeconds(), props);
			}
			else if (toValues.length > 0)
			{
				props = getVarsObject(TwoonFromToType.TO);
				tween = TweenLite.to(target, getDurationInSeconds(), props);
			}
		}

		override protected function getVarsObject(direction:TwoonFromToType = null):Object
		{
			var res:Object = super.getVarsObject(direction);
			res.ease = getEasingName();
			var value:TwoonValue;
			switch(direction)
			{
				case TwoonFromToType.FROM:
					var fromValues:Array = getFromValues();
					if (fromValues.length > 0)
					{
						for each(value in fromValues)
						{
							res[value.property.name] = value.fromValue;
						}
					}
					break;
				
				case TwoonFromToType.TO:
					var toValues:Array = getToValues();
					if (toValues.length > 0)
					{
						for each(value in toValues)
						{
							res[value.property.name] = value.toValue;
						}
					}
					break;
			}
			if (!isNaN(delay)) res.delay = getDelayInSeconds();
			return res;
		}
		
		protected function getEasingName():String
		{
			// PENNER NAMING ?
			var ease:TwoonEasingType = (easing) ? easing : TwoonEasingType.CUBIC;
			var mvmt:TwoonEasingMovement = (movement) ? movement : TwoonEasingMovement.OUT;
			return ease.name + "." + mvmt.name;
		}
	}
}